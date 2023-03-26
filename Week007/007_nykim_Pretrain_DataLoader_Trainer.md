# Pretrain
## 1. DataLoader
- 문제점 1 : batch size 16으로 설정해도 2개만 나옴 -> len 길이 잘못 설정해서 나온 이슈. 해결
- 문제점 2 : decode_inputs에서 513개의 토큰이 나옴 -> data.py 내용 수정하여 적용해야 함
- Preprocessing text infilling에 적용했지만 원본에 적용하지 않아 문제될 것.

## 2. Trainer
HuggingFace Trainer를 이용한 코드 작성
```python
def main(self) :
        logging.set_verbosity_info()
        # logging.basicConfig(
        #     format="%(asctime)s - %(levelname)s - %(name)s - %(message)s",
        #     datefmt="%m/%d/%Y %H:%M:%S",
        #     handlers=[logging.StreamHandler(sys.stdout)]
        # )
        logger = logging.get_logger("PatentBART")
        logger.debug("DEBUG")

        training_args = Seq2SeqTrainingArguments(
            output_dir=self.args.output_dir,
            overwrite_output_dir=True,
            num_train_epochs=self.args.epoch,
            per_device_train_batch_size=self.args.batch_size,
            save_strategy='steps',
            save_steps=10000,
            save_total_limit=1,
            # learning rate scheduler, optimizer
            learning_rate=self.args.learning_rate,
            weight_decay=0.01,
            lr_scheduler_type='linear',
            # warmup_steps=0,
            # warmup_ratio=0.0
            predict_with_generate=True,
            fp16=True,
            dataloader_num_workers=self.args.num_workers,
            # evaluation
            evaluation_strategy='no',
            # logging
            log_level='debug',
            logging_dir=self.args.logging_dir,
            logging_strategy='steps',
            logging_steps=500

        )

        log_level = training_args.get_process_log_level()
        
        logger.setLevel(log_level)
        # datasets.utils.logging.set_verbosity(log_level)
        logging.set_verbosity(log_level)

        # training_args._n_gpu = self.args.gpus

        trainer = Seq2SeqTrainer(
            model=self.model,
            args=training_args,
            train_dataset=self.train_dataset,
            eval_dataset=self.eval_dataset,
            # data_collator=self.data_collator,
            compute_metrics=compute_metrics

        )

        trainer.get_train_dataloader(self.train_dataset)
        trainer.get_eval_dataloader(self.eval_dataset)

        trainer.train()
        # trainer.train(resume_from_checkpoint='path_to_ckpt')
        trainer.save_model(self.args.output_dir)
    
        trainer.evaluate(max_length=self.args.max_length)
```
- BART 모델은 Seq2Seq 모델이라 Seq2SeqTrainingArguments, Seq2SeqTrainer를 사용하여 parameter 설정

