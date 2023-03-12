https://www.inflearn.com/course/lecture?courseSlug=%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8&unitId=49576
- 정적 컨텐츠
- MVC와 템플릿 엔진
- API

data drive test case...
- FIO: FIO란? FIO는 Flexible I/O Tester의 약자로 읽기, 쓰기, IOPS, Bandwidth등의 결과를 나타내주어 성능을 측정하기 위한 Tool. 이 외에도 MLTT(라이센스 구매 필요), vdbench등등 있음. 이러한 툴들을 사용해 다양한 테스트케이스 워크로드 개발
- block device command: blkid, lsblk, fdisk, fstrim... 
- abnormal nvme cli command: fwdown, fwcommit, get feature, set feature, flush... nvme spec에 따라 option으로 비정상적인 값을 주었을 때 $? 시 fail되는것을 확인
- kernal check: dmesg
- lvm 실습
<create lvm mirror>

1. pvcreate
pvcreate /dev/nvme0n1
pvcreate /dev/nvme1n1
pvs -> pvcreate 확인

2. vgcreate
vgcreate mirror /dev/nvme0n1 /dev/nvme1n1
vgs -> vgcreate 확인

3. lvcreate
lvcreate -l 100%FREE -m 1 -n lv01 mirror /dev/nvme0n1 /dev/nvme1n1
-L: size
-m: 사본갯수
-n: lv_name
lvs -> lvcreate 확인
vgs -> lvcreate 확인

4. create filesystem
mkfs -t ext4 /dev/mapper/mirror-lv01
file -s /dev/mapper/mirror-lv01 -> filesystem 확인
file -s /dev/dm-4 -> filesystem 확인

5. mount
mkdir -p /lvm/mirror
mount /dev/mapper/mirror-lv01 /lvm/mirror
df -h -> mount 확인

6. mount한 lvm filesystem에 다양한 워크로드 실행 가능. mirror/linear일 때 i/o들어가는게 다른데, mirror의 경우 디바이스에 들어가는 i/o들이 동일하고 linear일 경우 i/o수행되는 주 디바이스가 분리됨

<remove lvm mirror>

1. umount
umount /lvm/mirror
df -h -> umount 확인

2. vgremove 
vgremove mirror

3. pvremove
pvremove /dev/nvme0n1
pvremove /dev/nvme1n2
blkid -> remove된 것 확인