### Node 개요  
#### 1. Node 의 등장 배경  
=>웹의 대중화  
=>웹 브라우저에 대해서 친숙해지고 웹 브라우저 안에서 모든 작업을 하기를 원함  

=>웹 클라이언트 & 서버 개발  

웹 브라우저 출력(HTML, CSS, JavaScript)  

동적인 내용을 출력하도록 하기 위한 서버(데이터 저장은 RDBMS-Oracle, MySQL, MSSQL, Postgress SQL 등, 동적인 처리는 VB 기반의 ASP, PHP, Java 기반의 JSP, Ruby 등)  

=>스마트 디바이스의 등장  
개발자가 아닌 사람들이 애플리케이션 개발에 동참  

=>Mongo DB, Express, Angular(React), Node - MEAN(MERN)
서버 와 클라이언트의 개발을 하나의 언어만 배워서 구현
Mongo DB(NoSQL - BSON), Node(Java Script를 이용해서 Application 개발), Express(Node를 이용해서 웹 서버를 쉽게 구축), Angular(React, Vue 등)

#### 2.개발 환경 구축  
1) node.js 설치  
=>https://nodejs.org 에서 다운로드 받아서 설치  
=>node의 경우는 안정적인 버전 뒤에 LTS 라는 단어가 붙으며 홀수 버전은 시험판  
=>설치 확인  
cmd(shell, terminal)에서 node 라고 입력했을 때 버전 정보 와 프로프트가 > 로 바뀌면 됩니다.  

2) node.js를 코딩하고 해석하고 실행하기 위한 IDE 가 필요  
=>텍스트 편집기 와 node.js 만 설치되어 있어도 가능  
=>저는 수업 시간에 VS Code 사용  
=>다운로드:https://code.visualstudio.com/download  

#### 3.프로젝트 생성 및 실행  
1) 프로젝트에서 사용할 디렉토리를 생성  

2) vscode를 실행해서 생성한 디렉토리 열기  

3) 터미널에 npm init 이라는 명령을 수행하고 옵션을 설정  
=>터미널 열기: [View] - [Terminal]  

=>옵션을 성공적으로 수행하면 package.json(maven 의 pom.xml 파일 gradle의 build.gradle 파일 과 유사 - 프로젝트의 의존성을 설정하는 파일) 파일이 프로젝트에 생성  

4) 프로젝트에 js 파일을 생성(index.js)하고 작성  
```javascript
console.log('Hello Node.js')  
```  

5) 실행  
=>터미널에서 node 파일명  
실행을 한 후 터미널을 확인해보면 console.log에 작성한 내용이 출력됩니다.  

#### 4.모듈 프로그래밍 - 나누어서 프로그래밍  
=>파일을 나누어서 작성하는 방식  
=>하나의 파일에 모두 작성해도 실행은 되지만 이렇게 하면 가독성이 떨어지고 유지보수가 어려워집니다.  
이런 문제점을 해결하기 위해서 동일한 역할을 수행하는 내용을 파일 별로 나누어서 프로그래밍 합니다.  
발전된 형태가 객체 지향 프로그래밍 입니다.  
자바스크립트에서는 클래스를 만들 수 없고 TypeScript를 이용하면 클래스를 생성할 수 있습니다.  

1) 모듈 작성  
=>자바스크립트 파일을 만들고 다른 곳에서 사용 가능한 변수나 함수를 module.exports = { } 안에 나열  

2) 모듈 사용  
변수명이나 함수명 나열 = require('모듈 이름')  

3) 실습  
=>var.js 파일로 다른 곳에서 사용할 변수를 생성하고 내보내기  
```javascript
const odd = '홀수'
const even = '짝수'

module.exports = {
    odd, even
}
```  
