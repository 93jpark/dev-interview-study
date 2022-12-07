# 웹 브라우저의 렌더링 
웹 페이지는 미리 만들어진 것을 가져오는 것이 아니라 실시간으로 그려지는 것에 가깝다. 실시간으로 웹사이트가 그려지는 과정, 이 과정을 웹 브라우저의 렌더링 과정이라고 말한다.

* 파싱(parsing): 프로그래밍 언어로 작성된 파일을 실행시키기 위해 구문 분석을(syntax analysis)을 하는 단계이다. 파일의 문자열들을 문법적 의미를 갖는 최소 단위인 토큰으로 분해하고, 이 토큰들을 문법적 의미와 구조에 따라 노드라는 요소로 만든다. 노드들은 상하관계를 반영해 트리를 형성하는데, 이 트리를 파스트리라고 한다.

## 렌더링(rendering)

**HTML, CSS, JavaScript 파일을 파싱해, 브라우저에 시각적으로 출력하는 과정**

### 브라우저 렌더링 전체 과정

모든 웹 브라우저는 렌더링 엔진과 자바스크립트 엔진을 갖고 있다. 렌더링 엔진은 HTML, CSS 문서를 읽어내 실제 웹사이트의 모습을 그려내준다.

1. 브라우저는 HTML, CSS, JS, 이미지, 폰트 등 **리소스를 서버에 요청하고, 응답으로 받아온다.**
2. 브라우저 **렌더링 엔진**은 **받아온 HTML, CSS를 파싱**해 **DOM, CSSOM을 생성하고, 이들을 결합해 렌더 트리를 생성한다.**
3. 브라우저 **JS엔진**은 **받아온 JS를 파싱해 AST(Abstract Syntax Tree)를 생성하고, 바이트코드로 변환해 실행한다.**(이때 JS는 DOM API를 통해 DOM이나 CSSOM을 변경할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.)
4. 렌더트리를 기반으로 HTML 요소의 레이아웃(위치, 크기)을 계산한다.
5. 화면에 HTML요소를 페인팅한다. 


## 1.요청과 응답

>step1. 브라우저는 HTML, CSS, JS, 이미지, 폰트 등 리소스를 서버에 요청하고, 응답으로 받아온다.

서버에 요청은 어떻게 전송할까? 브라우저에 있는 **주소창**이 그 역할을 한다. 

주소창에 URL입력하고 엔터키를 누르면, URL의 호스트 이름이 DNS(도메인 네임 서비스)를 통해 진짜 주소인 IP주소로 변환되고, 이 IP 주소를 갖는 서버에게 요청을 보낸다. 

**URI 구조**
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhMA8N%2Fbtry4f4Jv63%2FMCmJqvqqEMp4U9MYE5U3f0%2Fimg.png)


![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKg2J5%2Fbtry8y9PjAd%2FsX4LXaJJ5T8GRhNh5leKw0%2Fimg.png)

서버는 기본적으로 보통 index.html을 응답으로 주도록 설정되어 있다.  예를들어, 우리가 https://www.google.com 을 검색하면, 
사실은 https://www.google.com/index.html 을 요청하는 것과 다름 없다. 이 요청에 대해 구글 서버는 클라이언트에 index.html 파일을 전달해줄 것이다. 다른 파일을 요청하고싶다면 뒤에 다른 파일 경로를 적거나, Javascript를 통해서 동적으로 요청할 수도 있다. 요청과 응답은 개발자 도구 Network 패널에서 확인할 수 있다.

**index.html뿐 아니라 css, js, 이미지, 폰트 파일들도 같이 응답하는 이유는 브라우저 렌더링 엔진이 HTML을 파싱하는 도중 외부 리소스를 로드하는 태그(link, img, script 등)를 만나면 HTML 파싱을 일시 중단하고 해당 리소스 파일을 서버로 요청하기 때문이다.**

## 2-1.HTML 파싱, DOM 생성
>step2. 브라우저 렌더링 엔진은 받아온 HTML, CSS를 파싱해 DOM, CSSOM을 생성하고, 이들을 결합해 렌더 트리를 생성한다.

서버가 응답한 HTML 문서는 오직 텍스트만으로 이루어져있다. 이 문서를 브라우저에 시각적인 픽셀로 렌더링 하려면 HTML 문서를 브라우저가 이해할 수 있는 형태로 바꾸는 작업이 필요한데, 그 형태가 바로 DOM구조이다. 

1. 바이트(Bytes) : 서버는 브라우저에게 **2진수 형태의 HTML 문서를 응답으로 준다.**

2. 문자열(Characters) : 문서는 **meta태그의 charset 속성에 지정된 방식으로 문자열로 인코딩 된다.**(ex. UTF-8) 서버는 이 인코딩 방식은 응답 헤더에 담아준다.

3. 토큰(Tokens) : 문자열 형태의 HTML문서를 **'토큰'단위로 분해**한다. (문법적 의미를 갖는 코드의 최소 단위) 

4. 노드(Nodes) : 각 토큰을 **객체로 변환해, 노드를 생성한다.** (DOM을 구성하는 기본 요소) 

5. DOM : **HTML문서의 요소들의 중첩관계**를 기반으로 노드들을 **트리 구조**로 구성한다. 이 트리를 **DOM(Document Object Model)** 이라고 한다.
(말 그대로 문서를 객체로 바꾼 모델을 의미)

   ![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd752eh%2Fbtry8y211Yn%2FjXqSArXalZzp1tpeg9Vee0%2Fimg.png)

## 2-2. CSS 파싱, CSSOM 생성

앞서 HTML을 파싱하는 도중 외부 리소스를 로드하는 태그(link, img, script 등)를 만나면 HTML 파싱을 일시 중단하고 해당 리소스 파일을 서버로 요청한다고 언급했었다. 

이 태그들은 CSS 파일을 가져올 때 보통 쓰는데, 이렇게 가져온 CSS파일도 HTML과 동일한 파싱과정(바이트->문자->토큰->노드->CSSOM)을 거치며 해석하여 CSSOM(CSS Object Model)을 생성한다. 

CSSOM을 생성하고 나면, 파싱이 중단된 지점부터 다시 HTML 파일은 파싱하기 시작해 DOM생성을 재개한다. 조금 다른 점은 CSS의 상속을 반영하여 생성된다.

   ![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdf1gLS%2Fbtry4gCALFm%2FiSKf1mkVTPH04K02o0YAA0%2Fimg.png)

## 2-3.렌더 트리 생성 

DOM과 CSSOM은 굉장히 비슷하게 생겼지만, 서로 다른 속성들을 가진 독립적인 트리들이다. HTML은 구조를, CSS는 디자인을 담당하기 때문에 둘을 합치는 작업이 필요하다. 

렌더 트리는 렌더링을 목적으로 만드는 트리로, 브라우저가 사용자에게 보여주기 위한 화면을 그리기 위한 과정으로, 보이지 않을 요소들은 이 트리에 포함하지 않는다. DOM과 CSSOM은 렌더링을 위해 렌더 트리로 결합된다.  

   ![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdpJAcH%2Fbtry7r4olZc%2FrCgtlnvK2UjosAEUpR0Nq1%2Fimg.png)


렌더 트리는 아직까지 텍스트로 구성된 객체로밖에 보이지 않는다. 실제로 우리가 보는 페이지를 만들기 위해서는 페인팅 작업을 거쳐야한다. 

## 3.JavaScript 파싱 

>step3. 브라우저 JS엔진은 받아온 JS를 파싱해 AST(Abstract Syntax Tree)를 생성하고, 바이트코드로 변환해 실행한다.

렌더링 엔진은 HTML 파일을 한줄씩 파싱하며 DOM을 생성하다가 Javascript 코드들 불러오는 script 태그를 만날 때도 파싱을 잠시 멈춘다. 그리고나서 src 속성에 적혀있는 파일을 서버에 요청해 받아온다. 이렇게 받아온 js파일도 마찬가지로 파싱을 해야하는데, 이 파싱은 브라우저 렌더링 엔진이 직접하지 않고, Javascript 엔진이 담당하게 된다. 이 때 렌더링 엔진은 JS엔진에게 제어권을 아예 넘겨주기 때문에, HTML 파싱을 멈췄다가 js파싱이 다되면 다시 제어권을 돌려받아 파싱을 다시 시작하는 것이다.

JS엔진은 js파일의 코드를 파싱해서 컴퓨터가 이해할 수 있는 기계어로 변환하고 실행한다. 좀 더 구체적으로 살펴보면, 먼저 단순한 텍스트 문자열인 코드를 토큰 단위로 분해한다. 이렇게 분해된 토큰에 문법적인 의미와 구조가 더해져, AST(추상 구문 트리) 라는 트리가 완성된다. 이를 기반으로 인터프리터가 실행할 수 있는 중간 코드인 바이트코드를 생성하여 실행한다.  
>LHS(left hand side): 다른 변수값을 지정하여 저장할 변수
>RHS(right hand side): 다른 변수에 저장될 변수값에 해당하는 변수

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FchkIMn%2Fbtry8izp0Wz%2F4TsRT9TO6Unf8XIUxKhzE0%2Fimg.png)

## 4.레이아웃(리플로우)
>step4. 렌더트리를 기반으로 HTML 요소의 레이아웃(위치, 크기)을 계산한다. 

렌더트리에는 요소들의 위치, 크기와 관련된 정보들이 들어있다. 하지만 전체화면에서 정확히 어디에 위치할 것인지에 대해서 잘 알지 못하기 때문에 이런 계산을 하는 단계가 레이아웃 단계이다. 노드 추가/삭제, 요소의 크기/위치 변경, 윈도우 리사이징 등 레이아웃에 영향을 주는 변경이 발생한 경우에 한하여 실행된다. 브라우저는 렌더트리의 맨 윗부분부터 아래로 내려가며 계산을 진행한다. **모든 값들은 절대적인 단위인 px값으로 변환된다.**
예를 들어 우리가 div요소 하나만 띄우도록 코드를 작성했고, width를 50%로 지정해두었다면, 이 값은 전체 화면 크기(viewport)의 절반 크기로 계산되고, 절대적인 값인 px 단위로 변환되는 식이다.

## 5.페인팅
>step5. 화면에 HTML요소를 페인팅한다. 

화면에 색상을 입히고, **어떤 요소를 보여주기 위해서는 이 픽셀에 대한 정보가 있어야 한다.** 페인팅은 이러한 픽셀들을 채워나가는 과정이다. 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbriyci%2Fbtry66TJNy6%2FSUVzSATWwqK0kruOy55SFK%2Fimg.png)

* 리플로우: 레이아웃 다시 계산하는것.
* 리페인팅: 새로운 렌더트리를 바탕으로 다시 페인트를 하는 것
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbq8I4z%2Fbtry7vsvVpZ%2F1eRxOyArCa7djYsVtuzNt1%2Fimg.png)

## script 태그의 async/defer 어트리뷰트

* 자바스크립트 파싱에 의한 DOM 생성 중단 문제를 근본적으로 해결하기 위해 HTML5부터 script 태그에 async와 defer 어트리뷰트가 추가되었다.
* async, defer 어트리뷰트는 다음과 같이 src 어트리뷰트를 통해 외부 자바스크립트 파일을 로드하는 경우에만 사용할 수 있다. (인라인 자바스크립트는 사용 불가능)

```html 
 <script async src="extern.js"></script>
```

* async와 defer 어트리뷰트를 사용하면 HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행되지만, 자바스크립트 실행 시점에 차이가 있다.

**async 어트리뷰트**
* HTML 파싱, 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다.
* 단, 자바스크립트의 파싱과 실행은 **자바스크립트 파일의 로드가 완료된 직후 진행되며, 이때 HTML 파싱이 중단된다.**
* 여러 개의 script 태그에 async 어트리뷰트를 지정하면 script 태그 순서 상관없이 로드가 완료된 자바스크립트부터 먼저 실행되므로 순서가 보장되지 않는다.
* 따라서 순서 보장이 필요한 scritp 태그에는 async 어트리뷰트를 지정하지 않아야 한다.
* IE10 이상에서 지원된다.

**defer 어트리뷰트**
* HTML 파싱, 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다.
* 단, 자바스크립트의 파싱과 실행은 HTML 파싱이 완료된 직후, 즉 DOM 생성이 완료된 직후(이때 DOMContentLoaded 이벤트가 발생한다) 진행된다.
* 따라서 DOM 생성이 완료된 이후 실행되어야 할 자바스크립트에 유용하다.
* IE10 이상에서 지원된다.

