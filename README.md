
CSS 방법론 (OOCSS, BEM, SMACSS) 자료 정리

# CSS 방법론
* CSS 설계의 중요성
* OOCSS
* BEM
* SMACSS

# CSS 설계의 중요성
## CSS 개발의 문제점
CSS를 작성하는 것이 쉽지만 한 번 확장하고 관리하기는 어려움
* CSS의 전역환경
* 일관적이지 않은 코드 구조, 각자 다른 사고 방식 스타일 정의
* 지나치게 복잡한 선택자
* 동일 요소에 대한 중복 설정, 불필요한 CSS의 증가
* CSS 셀렉터 우선순위 or !important 사용
* CSS (표현), JS (동작), HTML (내용) 간 명확한 분리가 안됨 (높은 결합도)

## 사이트 규모가 커질수록..
유지 보수가 불가능한 코드 -> 귀차니즘, 중복, 코드분석 시간 -> 새로운 기능의 개발 속도 저하

## CSS 작성 방법
* 적절한 의미 사용 (시맨틱)
* 중첩 선택자
* 모듈화
* 명명 규칙

## 적절한 의미 사용 (시맨틱)
HTML에서 시맨틱은 적절한 마크업 태그 사용
```html
<!-- Bad -->
<div class="footer"> ... </div>

<!-- Good -->
<footer"> ... </footer>
```

## 의미론적 CSS
* 컨텐츠의 성격과 기능을 전달하는 클래스명
* 이해하기 쉬운 클래스명
* 시맨틱 CSS는 훨씬 더 추상적이고 주관적

## 중첩 선택자
만약 선택자가 이렇게 길어진다면, 다음과 같은 CSS를 작성하고 있을 가능성이 높음

```css
.container .content .profile { ... }
```
* HTML과 밀접하게 엮여있다.
* 너무 구체적이다.
* 재사용할 수 없다.

## 특정도 평준화
더 높은 우선순위 싸움 → 악순환

<table class="table">
  <thead>
  <tr class="header">
    <th>Selector</th>
    <th>ID (a)</th>
    <th>Classes (b)</th>
    <th>Elements (c)</th>
    <th>Specificity (a-b-c)</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td>p</td>
    <td style="text-align:center">0</td>
    <td style="text-align:center">0</td>
    <td style="text-align:center">1</td>
    <td style="text-align:center">0-0-1</td>
  </tr>
  <tr>
    <td>p#foo</td>
    <td style="text-align:center">1</td>
    <td style="text-align:center">0</td>
    <td style="text-align:center">1</td>
    <td style="text-align:center">1-0-1</td>
  </tr>
  <tr>
    <td>p.bar1</td>
    <td style="text-align:center">0</td>
    <td style="text-align:center">1</td>
    <td style="text-align:center">1</td>
    <td style="text-align:center">0-1-1</td>
    </tr>
  <tr>
    <td>p.bar1.bar2.bar3</td>
    <td style="text-align:center">0</td>
    <td style="text-align:center">3</td>
    <td style="text-align:center">1</td>
    <td style="text-align:center">0-3-1</td>
  </tr>
  </tbody>
</table>

## 모듈화
* 디자인을 구성 요소(component)로 분해
* 코드가 분리 될수록 클래스 간 상호 의존성이 낮음
* id 보다 class를 활용 (재사용 불가능)
* 태그 선택자의 사용을 지양

## 명명 규칙
쉬운 유지보수, 코드의 재사용, 확장 가능, 직관적인 네이밍을 고려한 설계 방법
* OOCSS (Object Oriented CSS)
* BEM (Block Element Modifier)
* SMACSS (Scalable and Modular Architecture for CSS)

# OOCSS (Object Oriented CSS)

## OOCSS의 2가지 원칙
OOCSS는 객체 지향에 따라 고안된 설계 방식
* 구조와 외형의 분리 (Separate structure and skin)
* 컨테이너와 내용 분리 (Separate container and content)

## 구조와 외형의 분리
기본적인 구조와 반복 정의되는 외형은 따로 정의 (공통 스타일 추상화)
* 구조 : width, height, border, padding, margin
* 외형 : color, border-color, font-color, background-color


```html
<a href="#" class="blackborder bluebg">장바구니</a>
<a href="#" class="blackborder redbg">바로구매</a>
```
```css
.body_em .btn_wrap .redbg {
  background-color: yellow;
}
```
* 유연하게 사용가능
* 재사용성을 확보하는 이름
* 클래스명에 의미를 갖게 할 것 (시맨틱)

## 의미론적 CSS
DRY (Don't Repeat Yourself) CSS
```html
<a href="#" class="cartbtn">장바구니</a>
<a href="#" class="buybtn">바로구매</a>
```
```css
.cartbtn{
  display:inline-block;
  padding:10px 20px;
  color:#fff;
  border:3px solid #000;
  border-radius:10px;
  background-color:blue
}
.buybtn{
  display:inline-block;
  padding:10px 20px;
  color:#fff;
  border:3px solid #000;
  border-radius:10px;
  background-color:red
}
```

## OOCSS Style
기본 구조가 독립적으로 지정되어 있기 때문에 향후 다른 색의 버튼이 추가되더라도 외형 스타일만 추가로 정의
```html
  <a href="#" class="btnbase cart">장바구니</a>
  <a href="#" class="btnbase buy">바로구매</a>
```
```css
/* 버튼 구조: 공통적인 구조 지정 */
.btnbase{
  display:inline-block;
  padding:10px 20px;
  color:#fff;
  border:3px solid #000;
  border-radius:10px;
}
/* 버튼 외형 */
.cart{
  background-color:blue
}
.buy{
  background-color:red
}
```

## 컨테이너와 내용의 분리
* 위치에 의존하지 않는 스타일 정의
* 어떤 태그라도 동일한 외형 제공
* 어디에서나 재사용이 가능한 클래스 기반 모듈 구축

### 태그에 스타일 지정
```html
<!-- Bad -->
<h2> ... </h2>
```
```css
h2 { font-size:16px }
```
### 클래스명을 부여하고 스타일 지정
태그가 변경되어도 CSS를 바꿀 필요가 없음
```html
<!-- Good -->
<h3 class="subtitle"> ... </h3>
<span class="subtitle"> ... </span>
```
```css
.subtitle { font-size:16px }
```

### 장소를 한정하고 스타일 지정
```css
.header .logo {
  background-image:url(img/logo.png);
  width: 250px;
  height: 25px;
}

.footer .logo {
  background-image:url(img/logo-small.png);
  width: 100px;
  height: 15px;
}
```
### 종속되지 않는 클래스명을 부여하고 스타일 지정
구조적 상황에 관계없이 문서 어느 곳에서나 재사용 가능
```css
.logo-large {
  background-image:url(img/logo.png);
  width: 250px;
  height: 25px;
}

.logo-small {
  background-image:url(img/logo-small.png);
  width: 100px;
  height:15px;
}
```

## OOCSS 장/단점
* 좋은 점 : 재사용함으로써 코드 양을 줄임 (DRY 원칙)
* 나쁜 점 : 특정 요소의 스타일 변경 시 대부분 클래스가 공통적이기 때문에 CSS뿐만 아니라 마크업에 클래스를 추가해야 할 가능성이 높음

# BEM (Block Element Modifier)
CSS 클래스를 구조화, 이름을 지정, 코드의 유연성과 유지 관리 가능성을 높이는 방법
* Block, Element, Modifier로 나누어 클래스명 기술
* 엄격한 명명 규칙이 특징 (class만 사용. ID, 태그 사용 금지)
* 클래스명이 용도, 형태를 의미하므로 직관적인 것이 장점, 길고 복잡해지는 것이 단점

## Block
* 재사용 가능한 컴포넌트 (코드의 구조적 덩어리)
* 클래스명은 하나의 단어 사용, 길어질 경우 단일 하이픈(-)으로 구분
* ex) logo / login form / navigation / header / footer

<img src="img/stick_man_b.png" width="60%">

```html
<div class="stick-man"> ... </div>
```
```css         
.stick-man { ... }
```

## Element
* 블록 외부에서 사용할 수 없는 블록내의 구성 요소
* 블록 맥락에서만 의미가 있어야 함
* 클래스명은 해당 블록 이름과 밑줄 두 개(__) 추가 후 작성

<img src="img/stick_man_e.png" width="60%">

```html
<div class="stick-man">
  <div class="stick-man__head"></div>
  <div class="stick-man__arms"></div>
  <div class="stick-man__feet"></div>
</div>
```
```css
/* Good */
.stick-man__head { ... }
.stick-man__arms { ... }
.stick-man__feet { ... }

/* Bad: 의존성 X */
.stick-man .stick-man__head { ... }
div.stick-man__head { ... }
```

## 깊이 최소화
요소의 요소를 만들 필요가 있다면 (block__element__element)

DOM 트리를 모방 하려고 하지 마세요

```html
<!-- Bad -->
<div class="stick-man">
  ...
  <div class="stick-man__arms">
    <span class="stick-man__arms__left"></span>
    <span class="stick-man__arms__right"></span>
  </div>
  ...
</div>
```

## 새로운 블록 만들기
```html
<!-- Good -->
<div class="stick-man">
  ...
  <div class="arms">
    <span class="arms__left"></span>
    <span class="arms__right"></span>
  </span>
  ...
</div>
```

```html
<!-- Bad -->
<div class="stick-man">
  ...
  <div class="stick-man-arms">
    <span class="stick-man-arms__left"></span>
    <span class="stick-man-arms__right"></span>
  </div>
  ...
</div>

<!-- 블록 이동을 시도 할 때, 이상한 이름으로 문제 발생 -->
<div class="iron-man">
  ...
  <div class="stick-man-arms">
    <span class="stick-man-arms__left"></span>
    <span class="stick-man-arms__right"></span>
  </div>
  ...
</div>
```

## 하나의 중첩된 요소로 BEM-트리 만들기
```html
<!-- Good -->
<div class="stick-man">
  ...
  <div class="stick-man__arms">
    <span class="stick-man__left"></span>
    <span class="stick-man__right"></span>
  </div>
  ...
</div>
```

## DOM 트리
```html
<ul>
  <li>
    <a>
      <span></span>
    </a>
  </li>
</ul>    
```
```css
.ul {}
.ul > li {}
.ul > li > a {}
.ul > li > a > span {}
```

## BEM 트리
```html
<ul class="menu">
  <li class="menu__item">
    <a class="menu__link">
      <span class="menu__text"></span>
    </a>
  </li>
</ul>
```
```css
.menu {}
.menu__item {}
.menu__link {}
.menu__text {}
```

## Modifier
* 블록, 요소에 대해 추가 변형을 제공 (외형, 상태)
* 클래스명은 블록 또는 요소 이름 옆에 하이픈 두 개(--) 추가 후 작성

### Block modifier
<img src="img/stick_man_m.png" width="60%">

```html
<div class="stick-man stick-man--blue"> ... </div>
<div class="stick-man stick-man--red"> ... </div>
```                  
```css
.stick-man--blue { ... }
.stick-man--red { ... }
```

### Element modifier
<img src="img/stick_man_m2.png" width="60%">

```html
<div class="stick-man">
  <div class="stick-man__head stick-man__head--small"></div>
  또는..
  <div class="stick-man__head stick-man__head--big"></div>
</div>                   
```                  
```css
.stick-man__head--small { ... }
.stick-man__head--big { ... }
```

# SMACSS (Scalable and Modular Architecture for CSS)
CSS를 모듈화하고 확장 가능하게 만드는 것을 목표

* OOCSS, BEM의 핵심 컨셉을 차용하고 좀 더 자세한 사항 추가
* 클래스명을 통한 예측, 재사용, 쉬운 유지보수, 확장성을 통해 스타일 체계화

## SMACSS의 핵심은 분류
5개의 구분된 카테고리로 CSS 코딩 기법 제시. 어떤 카테고리에 스타일이 속하는지 결정하는데 숙고 요구

* Base - 기본 규칙
* Layout - 레이아웃 규칙
* Module - 모듈 규칙
* State - 상태 규칙
* Theme - 테마 규칙


## Base - 기본 규칙
* 각 브라우저의 스타일을 초기화 시키는 목적으로 사용
* 요소(elements) 스타일의 기본값 지정 (reset.css, normalize.css)
```css
body,p,h1,h2,h3,h4,h5,h6,ul,ol,li,dl,dt,dd,table,th,td,form,fieldset,legend,input,
textarea,button,select{margin:0;padding:0}
body,input,textarea,select,button,table{font-family:AppleGothic,'돋움',Dotum,sans-serif;font-size:14px;line-height:1.25}
```

## Layout - 레이아웃 규칙
* 큰 틀의 레이아웃, 페이지의 다양한 요소를 배치, 구별하는데 사용
* 주요 컴포넌트 : header, footer, content, aside.. etc
* 하위 컴포넌트 : 주요 컴포넌트 내에 있는 컴포넌트 (nav, item list, form.. etc)
* 주요 컴포넌트는 id 셀렉터, 하위 컴포넌트 class 셀렉터로 스타일 작성
* 클래스명은 접두사로 l-, layout- 명시 요구
* ex) l-fixed 유무에 따라 가변 폭으로 할지 고정 폭으로 할지 결정하는 레이아웃

```css
#content {width:80%;float:left}
#aside {width:20%}

.l-fixed #content {
  width: 600px;
  margin-right: 10px;
}
.l-fixed #aside {
  width: 200px
}
```

## Module - 모듈 규칙
* 페이지에서 재사용 가능한 구성요소 (버튼, 위젯, 배너.. 등)
* 모듈은 레이아웃 구성요소 안에 존재 하지만 다른 모듈에도 존재 할 수 있음
* 각 모듈은 독립형으로 존재하도록 설계
* 재사용을 위해 CSS선택자로 id, 태그를 사용하지 않음

```html
<div class="box">
  <span class="box-name"> ... </span>
  <span class="box-items"> ... </span>
</div>
```                    
```css
.box { ... }
.box-name { ... }
.box-items { ... }
```

## State - 상태 규칙
* 요소의 상태 변화를 표현하는 스타일 (툴팁, 아코디언)
* 주로 Javascript으로 조작되는 클래스 지정
* 클래스명은 접두사로 is- 등을 명시 (is-hidden, is-collapsed)
* 모듈과 레이아웃 둘 다 적용 가능

```html
<!-- 레이아웃 요소, 접힌 상태 -->
<div id="header" class="is-collapsed">
  <form>
    <!-- 모듈, 오류 상태 -->
    <div class="msg is-error">
      There is an error!
    </div>
    <!-- 연관된 라벨이 숨겨진 상태 -->
    <label for="search" class="is-hidden">Search</label>
    <input type="text" id="search">
  </form>
</div>
```

## Theme - 테마 규칙
* 사용자가 테마를 선택할 수 있는 경우 사용
* 색상, 이미지를 불변하는 스타일과 분리 (background, color, border..)
* 메인 스타일 뒤에 읽어 들이게 하고 덮어쓰기를 하거나 기존 스타일을 재선언하여 사용
* theme- 등의 접두어를 명시 또는 theme/과 같은 디렉토리로 계층 분리
* 자주 사용되지는 않음

```css
/* main.css */
.box {
  border: 1px solid;
}
```
```css                        
/* theme.css - main.css 뒤에서 읽도록 */
.box {
  border-color: blue;
}
```

# 방법론은 방법론일 뿐..
보시다시피, 이러한 접근법 중에서 완벽하게 이상적인 것은 없음. 따라서 이 방법들 중 어느 것도 절대적인 규칙이 아님

# 정리
각각의 방법론에는 장/단점이 존재하기 때문에 프로젝트에 따라 나만의 방법론, 팀의 방법론을 만들어 가는것이 중요함