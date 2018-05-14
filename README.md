CSS방법론 (BEM, OOCSS, SMACSS)

http://www.risewill.co.jp/blog/archives/5652

CSS설계는 매우 중요한 것입니다.

일정한 규칙이 없으면 
각자가 다른 사고 방식에서 스타일 정의 하고 불필요한 CSS가 늘어나거나 
본인이 아니면 모르는 규칙이 발생해 유지보수 하기 어렵게 되어 버립니다.


그래서 다음을 의식하고 CSS 설계를 실시하는 것이 중요합니다.

예측 가능한
재사용 가능한
유지보수가 쉬운
확장 가능한

# OOCSS

## 요약
* Object Oriented CSS (객체 지향 CSS)
* 객체 지향에 따라 고안된 설계 방식
* Yahoo!의 Nicole Sulivan에 의해 개발  Twitter(Bootstrap), Github, Youtube에서도 사용

## 사고
* 구조와 외형, 또 컨테이너와 내용을 분리하여 클래스 정의하고 이를 조합하여 스타일을 정의하는 방법
* ID나 자식선택자에 의해 스타일을 정의하는 것이 아니라, 모든 스타일을 클래스로 정의하고 그것들을 조합


## 구조와 외형의 분리 (Separate structure and skin)
보편적인 구조와 반복 정의되는 외형은 따로 정의
구조와 외형을 분리하여 적은 코드로 더 모양을 정의 할 수 있습니다.

구조: width, height, border, padding, margin 등
스킨: color, border-color, background-color 등

```css
/* 버튼 구조(structure): 공통적인 구조 지정 */
.btn {
    width: 200px;
    height: 50px;
    line-height: 50px;
    text-align: center;
}
/* 버튼 외형(skin) */
.btn-blue {
    background-color: blue;
    color: white;
}
```

기본 구조가 독립적으로 지정되어 있기 때문에 향후 다른 색의 버튼이 추가되더라도 외형 스타일을 정의하는 것만으로 끝나네요

```html
<a class="btn btn-blue">파란색 버튼</a>
<a class="btn btn-red">빨간색 버튼</a>
<a class="btn btn-gray">회색 버튼</a>
```


디자인에 의해 구조 및 스킨 나누는 방법이 변경 될 수 있다고 생각합니다. 

둥근모양의 버튼이(border-radius) 공통적으로 사용되면 구조에 넣고 
버튼에 따라 다르게 적용해야 하는 부분은 스킨에 넣는 등 사이트 구성을 파악하고 유연하게 생각할 필요가 있습니다.


## 컨테이너와 내용의 분리 (Separate container and content)

HTML 요소와 구조, 구성 요소가 존재하는 '장소'에 의존하지 않는 CSS를 실현하기 위한 생각입니다.
CSS에 대응하는 HTML이 어떤 태그 이었다고해도 동일한 외형을 제공 할 수 있도록합니다.

```css
/* × 요소에 스타일을 지정 */
h2 { font-size:120%; }

/* ○ 클래스 이름을 부여하고 스타일을 지정 → 요소가 바뀌어도 CSS를 바꿀 필요가 없다 */
.subtitle { font-size:120%; }

/* × 장소를 한정하고 스타일을 지정 */
.header .logo {
  background-image:url(/img/logo.png);
  width: 250px;
  height: 25px;
}
.footer .logo {
  background-image:url(/img/logo-small.png);
  width: 100px;
  height: 15px;
}

/* ○ 클래스 이름을 부여하고 스타일을 지정 → 장소를 한정하지 않기 때문에, 사이드 바, 주요 지역에서도 사용가능 */
.logo-large {
  background-image:url(/img/logo.png);
  width: 250px;
  height: 25px;
}
.logo-small {
  background-image:url(/img/logo-small.png);
  width: 100px;
  height:15px;
}
```


# BEM
## 요약
* Block, Element, Modifier의 약어.
* HTML 구조를 명확하게 축을 둔 설계 도구 및 그 방법입니다. 
* 엄격한 명명 규칙이 특징, 클래스 이름이 길어 지므로, 경원하는 사람도 많습니다.
러시아 Yandex사에 의해 고안되었습니다.

## 사고
요소를 Block, Element, Modifier의 3 개로 나누어 명명 규칙을 바탕으로 Class 명을 기술합니다.

## 명명 규칙
"block__element-modifier"처럼 BEM은 "__" "_" "-"를 단어와 단어를 구분하는데 사용하고 
이를 세퍼레이터라고 부르고 있습니다. 
BEM은 Block, Element, Modifier 각각의 구분에 일관된 분리기를 사용하는 것이 중요합니다.



## Block
헤더 및 바닥 글·내비게이션 기사 검색 영역 등의 부품의 매수입니다. 
Block은 어디에나 둘 수 있고, Block에 Block을 포함 할 수도 있지만, 
CSS에서 Block을 중첩하여 스타일을 지정해서는 안됩니다. 
왜냐하면 Block은 완전히 독립적 어느 위치로 이동해도 단독으로 동작 할 필요가 있기 때문입니다.

Block과 Element의 구분은 "Block__Element"같이 밑줄 2 개로 연결합니다. 반드시 2 개 필요는 없지만, 
class 이름을 보는 것만으로 BEM을이용하고 있다고 알기 쉬우므로 2개 붙이는 것을 권장합니다.

```html
<div class="wrapper">　/*Block*/
　　<div class="header">　/*Block*/
　　　　<div>logo</div>　/*Block*/
　　</div>
　　<div class="mainarea">　/*Block*/
　　　　<section class="box">～</section>　/*Block*/
　　　　<section class="box box-white">～</section>　/*Block*/
　　　　<section class="box"><h2 class="box__title">～</p></section>　/*Block+Element*/
　　</div>
　　<div class="footer">～</div>　/*Block*/
</div>
```

## Element

Block 안의 하나 하나의 요소가 Element에 해당됩니다. 
기사라면 제목(h2)·기사 본문(p)등의 부분이 다 Element로 구성됩니다.
Modifier의 구분은 Element--Modifier 처럼 하이픈 2개로 연결합니다.

```html
<div class="search">　/*Block*/
　<a href="#" class="link">　/*Element*/
　<a href="#" class="link link--disabled">　/*Element+Modifier*/
</div>
```

## Modifier

같은 Block 또는 Element를, 색상, 크기를 바꾸는 등 다른 종류로 나눌 (파생) 때 사용합니다. 
다시 Element를 만드는 것이 아니라 Modifier(확장자)을 사용하여 파생시킵니다. 

이름 (key)와 값 (value)을 가지고 여러 Modifier를 동시에 사용할 수 있습니다. 

Block (또는 Element)와 Modifier의 key와 value의 구분은 Block_key_value 또는 Element_key_value 처럼 구분 기호에 밑줄 하나를 사용합니다.

예 : Block의 Modifier "Block_key_value"
```html
<ul class="list list_type_disc">
  <li class="list__item"></li>
  <li class="list__item"></li>
</ul>
  
<ul class="list list_type_none">
  <li class="list__item"></li>
  <li class="list__item"></li>
</ul>
```

예: Element의 Modifier "Element_key_value"
```html
<ul class="tubmenu">
  <li class="tubmenu__item"></li>
  <li class="tubmenu__item tubmenu__item_state_current"></li>
    <!-- ↑状態がcurrentであるというclass -->
  <li class="tubmenu__item"></li>
</ul>
```


# SMACSS
## 요약
Scalable and Modular Architecture for CSS의 약자. "스맥스 '라고 읽습니다.
OOCSS, BEM의 흐름을 수렴한 코딩 규칙. Jonathan Snook 씨에 의해 고안되었습니다.
CSS를 보다 체계적, 더 구조화시킴으로써 제작, 유지보수를 보다 쉽게 하는 것을 목표로 합니다.

## 사고
다음과 같은 5개의 규칙으로 구성

Base - 기본 규칙
Layout - 레이아웃 규칙
Module - 모듈 규칙
State - 상태 규칙
Theme - 테마 규칙


## Base - 기반 규칙
베이스는 사이트의 기본 스타일 설정에서 Reset.css과 Nomalize.css도 여기에 포함됩니다. 
사이트 전체 글꼴 크기와 줄 간격, a 요소의 글자 색과 : hover 등 태그에 직접 설정하는 것은 기본 규칙으로 설명합니다.


## Layout - 레이아웃 규칙
헤더 및 바닥 글·내비게이션 메인 컨텐츠·사이드 바 등 큰 틀의 레이아웃 규칙을 지정하는 규칙입니다.

명명 규칙
등급 지정에 접두어(layout-, l-)을 부여, 또는 ID를 부여하도록 SMACSS에서는 권장하고 있습니다.
※ID는 경우에 따라서는 CSS를 복잡하게 해버리므로 사용할 때는주의가 필요하지만 머리글과 바닥 글 등 범용 적으로 사용되는 ID도 있으므로, SMACSS는 ID 이용을 제한하지 않습니다.


```css
.l-main{
  width: 80%;
  float: left;
}

.l-fixed .l-main { /* px지정할 경우 body 태그 등에 l-fixed 클래스 부여 */
  width: 640px;
}
```





## Module - 모듈 규칙
모듈은 버튼과 텍스트, 탭 등 모든 재사용 가능한 부분을 가리킵니다.
클래스 이름은 모듈 이름-서브 클래스 이름의 순서로 씁니다.

명명 규칙
부모 모듈의 이름을 접두사로 부여합니다. 
클래스 이름은 div와 span 등으로 부여되지만 li, a 등은 반드시 부여 할 필요는 없습니다. 
제목은 h2 ← → h3 등의 변경이 일어나기 쉬우므로 클래스 이름으로 구분하는 것이 좋습니다.

```html
<div class="l-main">
  <div class="box">
    <h2 class="box-title">boxタイトル</h2>
    <p class="box-description">説明</p>
  </div>
</div>
```


## State - 상태 규칙
주로 javascript으로 조작되는 클래스를 지정합니다.
특정 상태에 따라 .is-disable, .is-active, .is-current 등을 부여하여 스타일을 덮어 씁니다.
예: 링크 입력 후, 비활성, 선택 시 등의 스타일

```html
<div class="l-main">
  <div class="box is-disable">
    <h2 class="box-title">boxタイトル</h2>
    <p class="box-description">説明</p>
  </div>
</div>
```
```css
.box.is-disable{
  display: none; /* is-disabled가 부여된 box는 숨김 */
}
```


## Theme - 테마 규칙
테마는 전체 스타일을 변경할 경우 사용하지만, 기회는 적을지도 모릅니다. 
메인 스타일의 뒤에 읽어 들이게 하고 스타일의 덮어쓰기를 하거나
클래스를 추가하고 뒤에서 스타일을 변경시키기도 합니다.


```css
/* main.css */
a {
  color: #00f;
}
.box {
  background-color: #fff;
}
```
```css
/* theme.css : main.css 뒤에서 읽도록 */
a {
  color: #f00;
}
.box {
  background-color: #eee;
}
```

# 정리
이번에 소개 한 설계 방법 이외에도 다양 하지만, 유명하다고 생각되는 것을 정리해 보았습니다. 
비교하면, OOCSS와 SMACSS는 멀티 클래스, BEM은 단일 클래스에 가까운 것인지라고 생각했습니다. 

규칙이 복잡한 것도 있으므로 처음에 제대로 설계하는 것이 중요합니다.

어떤 방법을 사용해도 좋다고 생각하고, 이를 바탕으로 기존 규칙을 만들어도 좋습니다. 
중요한 것은 팀이 그것을 공통 인식 할 수 있도록하는 것입니다. 

CSS뿐만 아니라 기술과 아이디어는 많이 있고, 점점 변해 갑니다. 
저도 옛날 자신이 만든 코드를보고 기절하는 경우도 많이 있습니다. 
과거의 자신을 부정하게되기도하지만, 두려워하지 말고 공부를 거듭해 가고 싶습니다.











# BEM
BEM은 블록（block）, 요소（element） 및 수정자（modifier）를 의미하며 Yandex 팀에서 제안한 프런트 엔드 명명 방법입니다. 
이 똑똑한 명명 방법은 CSS 클래스를 다른 개발자에게 더 투명하고 의미있게 만듭니다. 
BEM 명명 규칙은보다 엄격하며 시간이 많이 걸리는 대규모 프로젝트를 개발하는 데 필요한 정보를 더 많이 포함합니다.

내가 사용한 BEM 기반 명명법이 Nicolas Gallagher에 의해 수정되었음을 알아 두는 것이 중요합니다. 
이 기사에서 설명한 명명 기법은 원래 BEM이 아니지만, 내가 선호하는 개선 된 버전입니다. 
실제로 사용되는 기호의 종류와 관계없이 동일한 BEM 원칙을 기반으로합니다.

명명 규칙은 다음과 같습니다.
```css
.block{}  
.block__element{}  
.block--modifier{}  
```

.block은 더 높은 수준의 추상화 또는 구성 요소를 나타냅니다.
.block__element는 .block의 자손을 나타내며 전체적으로 완전한 .block을 형성하는 데 사용됩니다.
.block--modifier는 블록의 다른 상태 또는 다른 버전을 나타냅니다.

하이픈 대신 두 개의 하이픈과 밑줄을 사용하는 이유는 다음과 같이 단일 하이픈으로 구분 된 블록을 만드는 것입니다.



```css
.coupon-list{}
.coupon-list__field{}
.coupon-list--full{}
```

BEM의 핵심은 이름만으로도 다른 개발자에게 토큰이 무엇인지 말할 수 있다는 것입니다. 
HTML 코드에서 클래스 속성을 찾아 봄으로써 모듈이 어떻게 관련되어 있는지 이해할 수 있습니다. 
일부는 단지 구성 요소이고, 일부는 하위 구성 요소이거나 다른 구성 요소 또는 구성 요소입니다. 
문자. 우리는 유추 / 모델을 사용하여 다음 요소가 어떻게 관련되어 있는지 생각합니다.

```css
.person{}  
.person__hand{}  
.person--female{}  
.person--female__hand{}  
.person__hand--left{}   
```

아래는 일반적인 CSS로 작성한 것입니다.
```css
.person{}  
.hand{}  
.female{}  
.female-hand{}  
.left-hand{}
```

BEM (또는 BEM 변형)은 프런트 엔드 코드를 읽고 이해하고, 공동 작업을 더 쉽게하고, 제어하기 쉽고, 강력하고, 명확하고, 더 엄격하게 만드는 매우 유용하고 강력하며 간단한 명명 규칙입니다.


# OOCSS (Bootstrap)
말 그대로 객체 지향 CSS를 의미하는 [OOCSS] (Object Oriented CSS)는 Nicole Sullivan이 제안한 CSS 이론입니다. 
두 가지 주요 원칙은 다음과 같습니다.

* Separate structure and skin (별도의 구조와 테마)
* Separate container and content (별도의 container 및 content)

```html
<div class="media media-shadow">
    <div class="media-image-container">
        <img class="media-image" src="rean.jpg" alt="">
    </div>
    <div class="media-body">
        <p class="media-text">本作的主角，帝国北部地方贵族施瓦泽男爵的养子，也是托尔兹士官学校特科班“Ⅶ组”的成员。</p>
    </div>
</div>
```

```css
.media {
    padding: 10px;
}
.media:after {
    display: table;
    clear: both;
    content: " ";
}
.media-image-container {
    float: left;
    margin-right: 10px;
}
.media-image {
    display: block;
}
.media-body {
    overflow: hidden;
}
.media-shadow {
    box-shadow: 1px 1px 3px rgba(0, 0, 0, .5);
}
```


위 코드는 media이 배열을 나타내는 페이지 요소를 사용 합니다. HTML, CSS 및 자바스크립트 (있는 경우)를 전체적으로 구성하는 경우 구성 요소 또는 객체와 동일합니다. 
사이트의 어느 곳에서나 재사용 할 수 있습니다.

OOCSS의 두가지 원칙을 어떻게 구현할 것인가?



## 구조와 피부 분리 (Separate structure and skin)
분리 구조 및 테마 시각적 스타일 효과 (예 background) color별도의 "제목"로 적용. 
위의 예제에서 그림자 효과 media는 스타일 규칙 에 직접 기록되지 않지만 media-shadow라는 클래스에 별도로 기록됩니다. 
따라서 그것은 선택 가능하고 분리 가능한 주제가되었습니다. 
해당 테마가 필요하지 않은 경우 아무 것도 추가하지 말고 필요한 경우 해당 클래스를 추가

## 별도의 용기 및 내용물 (Separate container and content)
콘테이너와 콘텐트를 분리하려면 페이지 요소가 어디에 위치하는지에 의존하지 않아야합니다. 
위의 예제에서 css의 선택기는 매우 짧으며 상속 선택기가 없습니다 (예 :) .header .media`` { }. 따라서이 그래픽 배열의 요소는 어디에서나 사용할 수 있으며 모양이 일관됩니다.

이 구성 요소를 특정 위치에서 다르게 표시해야하는 경우이 구성 요소에 구성 가능한 옵션으로 "다른 부분"을 계속 추가하십시오. 
구성 요소의 모양은 여전히 ​​위치와 무관합니다.


## 사용방법
* class 늘리기
* 상속된 선택자를 사용하지 마십시오.

재사용을 추구하며 
클래스 이름은 상대적으로 추상적이며 
일반적으로 특정 내용을 반영하지 않습니다.



# SMACSS (Semantic UI)
SMACSS는 CSS 이론을 제안
주요 원칙은 3 가지입니다.

* Categorizing CSS Rules
* Naming Rules
* Minimizing the Depth of Applicability

이 원칙들은 무엇을 의미합니까?

## Categorizing CSS Rules
이것은 SMACSS의 핵심입니다. SMACSS는 css가 다음과 같은 5 가지 범주를 갖는 것으로 간주합니다.

1. Base
2. Layout（Major Components）
3. Module（Minor Components）
4. State
5. Theme




Base Rules, 모든 경우에 대해 페이지 요소의 기본 모양을 설명합니다. 
그것의 정의는 클래스와 ID를 사용하지 않는다. CSS reset 이 카테고리에 속합니다.

Layout Rules, 레이아웃 스타일 . 다음 모듈 규칙과 함께이 페이지의 특정 요소를 설명합니다. 이요소는 계층 적이며 레이아웃 규칙은 하위 모듈 규칙 요소의 컨테이너 역할을 할 수있는 상위 계층에 속합니다. 왼쪽 및 오른쪽 열, 그리드 시스템 등은 레이아웃 스타일의 일부입니다.

Module Rules, 모듈 스타일 . 제품 목록, 탐색 모음이 될 수 있습니다. 일반적으로 모듈 규칙에 의해 정의 된 요소는 앞서 언급 한 레이아웃 규칙 요소 내에 배치됩니다. 모듈은 독립적이며 다양한 경우에 재사용 할 수 있습니다.

State Rules, 특정 상태의 요소 모양을 설명합니다. 예를 들어, 메시지 상자가있을 수 있습니다 success및 error두 주하는 가질 수있는 탐색 모음 중 어느 하나의 current상태를.

OOCSS의 예를 계속하면 표시되지 않는 다음과 같은 새로 추가 된 요소가 is-hidden State Rules에 속합니다.

```html
<div class="media media-shadow is-hidden">
    ...
</div>
```

```css
.is-hidden{
    display: none;
}
```

Theme Rules, 테마 스타일 은 페이지 테마의 테마를 설명하며 일반적으로 색상, 배경 이미지를 나타냅니다. 
Theme Rules은 이전 4 개 카테고리의 스타일을 수정할 수 있으며 이전 4 개 카테고리 (전환하기 쉽도록 "피부 변경")와 분리되어야합니다.

SMACSS의 Theme Rules 즉, 당신이 Module Rules에서 정의 할 수있는 별도의 클래스 이름의 사용을 필요로하지 않는 .mod { }다음 또한 Theme Rules에서 사용 .mod { }수정할 부분을 정의 할 수 있습니다.


## Naming Rules

이 Naming Rules은 class의 이름 지정 등을 생각할 때 
이름 지정 스타일에 해당하는 범주를 사용하는 것을 고려한다는 것을 의미합니다.

상기 다섯 종류에 따라 분할 

Layout Rules l-또는 layout-이러한 프리픽스, 예를 들어 .l-header, .l-sidebar.

Module Rules 예를 들어 .media, .media-image.

State Rules 앞에 is-가 붙습니다 (예 : .is-active,,) .is-hidden.


Theme Rules - 접두사와 별도의 class, 같은 Theme Rules .theme-a-background, .theme-a-shadow.

Base Rules은 예를 들어 태그 선택기 지향적 인 스타일을 기반으로 
클래스와 ID를 사용하지 않습니다.
p, a 없이 명명.

이름 지정 규칙을 엄격하게 지킬 필요는 없으며 실제 조건과 선호도에 따라 다른 규칙을 만들 수 있습니다. 자신의 계약서 (문서 작성)를 기록하고이를 준수하는 것이 가능합니다.

## Minimizing the Depth of Applicability
리터럴 번역은 적응의 깊이를 최소화하는 것입니다.

```css
/* depth 1 */
.sidebar ul h3 { }

/* depth 2 */
.sub-title { }
```

위쪽 끝과 아래쪽 끝 사이의 차이는 html과 css 사이의 결합 정도 입니다
위 스타일 규칙은 상속 선택자를 사용하기 때문에 html의 구조에는 실제로 어떤 종속성이 있다고 생각할 수 있습니다. 

h3 요소를 다른 위치로 이동하면 더 이상 이러한 스타일을 사용할 수 없습니다. 
마찬가지로, 다음 스타일 규칙에는 선택기가 하나뿐이므로 특정 html 구조에 의존하지 않습니다. 
클래스에 요소를 추가하는 한 해당 스타일을 얻을 수 있습니다.

물론 선택기를 상속하는 것이 유용합니다. 동일한 이름으로 인해 발생하는 스타일 충돌을 줄일 수 있습니다 
(일반적으로 여러 사람 공동 작업 개발에서 발생). 
그러나 과도하게 사용해서는 안되며 가능한 한 짧은 형식의 html 구조 선택자를 사용하여 충돌하는 스타일을 유발하지 않아야합니다. 
이것은 SMACSS가 적응의 깊이를 최소화하는 것을 의미합니다.

이것은 OOCSS의 Separate container and content(용기 및 내용 분리 원칙)과 매우 유사합니다.



## 주요 목표
SMACSS는 두 가지 주요 목표 달성에 중점을 둡니다.

* 더 많은 의미 론적 HTML과 CSS
* 특정 HTML 구조에 대한 의존성 감소





---
https://www.monster-dive.com/blog/web_creative/20170525_000315.php

자, 이번에는 명명의 말씀입니다. 
아마 HTML이나 JS를 쓰는 사람이면 어느 있는 얘기라고 생각하지만 코드를 쓰기보다 클래스 이름을 보는 것이 귀찮게 느끼는 것 없어요? 
업계적으로는 여러가지로 논란이 다하고 있는 곳이기도 하지만, 결국 분명한 규칙은 없는 취향의 문제도 있으므로 고민이 없습니다.

아마도 HTML과 JS를 쓰는 사람이라면있는있는 이야기라고 생각 합니다만, 코드를 쓰기보다는 클래스 이름을 생각 게 귀찮게 느낄 것, 없습니까? 

결국 명확한 결정이 아니라 취향의 문제도 있기 때문에 고민도 끝이없는 것입니다.


## class 이름의 기본 규칙

* 알기 쉬운 영어 기반의 이름을 붙인다
너무 당연해하지만보고 난 그 요소의 성질이 전혀 상상할 수없는 이름은 NG. 
예를 들어 조금씩 장식의 다른 요소에 .block-1, .block-2, ...와 숫자를 흔들며 나가는 방식이라고 나중에봤을 때 혼란합니다. 

.block-noborder 라든지 .block-red 든가, 각각의 장식의 특징을 알 수있는 이름을 붙이는 것이다. 또 기본적으로는 이름은 영어로 붙인 것이 무난합니다. 

"통상 업무"에 대한 섹션에 이름을 넣으려고했을 때, .tsujogyomu인지 .tsujyogyomu인지 .tsujogyomu인지를 모르기 때문에 싫어한다는 것이 자신에게 이유입니다. 
영어라면 철자가 고유하게 결정테니까.

* 이름 통일감
명명하는 이라기보다는 설계 사상의 이야기입니다 만, 비슷한 성격을 가진은 이름에 어떤 연결을 갖게 싶은 곳입니다. 
예를 들어 카드 풍의 디자인이 여러 페이지에 존재하는 경우에 어떤 디자인이든 어느 클래스 이름에도 "card"라는 단어가 등장하는 것이 자연 스럽습니다. 
또 하이픈"-"언더파 스코어"_"은 다른 것으로써 혼재될 경우 반드시 취급의 차이를 명확히 합시다.


디자인 변경을 내다보고 명명한다

위의 요소에. foo-alpha로 명명하면서 디자인 변경으로. foo-beta의 아래로 이동이 되어 버렸다.
이 또한 있다. 
후출시 디자인 변경은 그만!라고 말하고 싶지 않을 수도 있지만 자신이 편안하기 때문에 일어날 것 같은 디자인 변경을 내다본 명명을 하는 것도 현자의 지혜입니다. 
개요의 요소에는 foo-summary, 본문에는. foo-content,는 식으로 요소의 본질을 대충 표현한 명명을 하면 다소의 디자인 변경에는 견딜 수 있는 HTML이 됩니다. 
사스 테나 부루 디자인이란 놈입니다.


* 디자인 변경을 내다보고 명명한다

왼쪽의 요소에. foo-left로 명명하면서 디자인 변경으로. foo-right과 좌우가 바뀌고 말았다.
위의 요소에. foo-alpha로 명명하면서 디자인 변경으로. foo-beta의 아래로 이동이 되어 버렸다.


후 내 디자인 변경은 그만! 라고 말하고 싶어 될지도 모르지만 자신이 편하게하기 위해 일어날 것 같은 디자인 변경을 예측 한 이름을 두는 것도 현명한 사람의 지혜입니다. 

개요의 요소에는 .foo-summary 본문에는 .foo-content, 등등 식으로 요소의 본질을 대충 표현한 명명을 하면 약간의 디자인 변경은 견딜 HTML됩니다. 


# 여러 명명 패턴
BEM이 유명하지만 요즘은 BEM을 확장한 규칙도 자주 봅니다. 
각각의 규칙에 대해서 장점/단점도 소개하겠습니다.

# OOCSS (Object Oriented CSS)

이른바 프로그래밍에서 객체 지향을 CSS설계에서도 활용하자라는 생각입니다. 
각각의 "요소"에 이름을 붙이는 것이 아니라 먼저"기능"과 "성질"에 이름을 지어
그 요소가 갖고 있다 "기능"과 "성질"만큼 클래스를 붙여 가고 있습니다.

```html
<div class="main">
    <div class="panel bordered wide"></div>
</div>
```

장점
* 이름을 붙이는 대상이 "기능"과 "성질"이라 이름을 생각하는 게 편하다.
* 하나 하나의 클래스 이름이 짧아진다.
단점
* 여러 클래스의 조합으로 스타일링하기 때문에, CSS가 복잡해진다.
* 예외에 약하다. 이곳은 마진 10px이지만 이쪽은 5px,라고 말하면 곤란하다.



# BEM
아마도 가장 주요 HTML / CSS 명명 규칙. 
"이름을 잘 표현하는"듯이, 하나의 클래스 이름에 최대한의 정보를 넣는 것이 특징입니다. 
__B = Block __ __ E = Element __ __ M = Modifier__의 약자로, 이들을 block__element - modifier 형태로 연결 한 것이 클래스 이름입니다.

Element 요소에서 Block은 그 요소의 덩어리. Modifier는 기본 스타일에서 파생 된 경우에 추가합니다.
```html
<div class="main">
    <div class="main__panel--bordered--wide"></div>
</div>
```

장점
* 하나의 클래스 이름으로 그 요소의 특성을 나타낼 수 있다.
* 요소마다 독특한(혹은 그것에 가까운)이름을 붙이게 되므로, CSS의 구조는 간단하게 된다.
* SASS 등의 전처리와 궁합이 좋다.

단점
* 클래스 이름이 길고 추하다.
* SASS 등의 전처리가 도입되지 않으면 CSS를 쓰는 것이 괴롭다.
* SASS의 mixin에 B/E/M을 연결하는 구조를 잘 보지만 실제 클래스 이름으로 검색하지 못하는 것은 불편하다고 생각한다.






# SMACSS (Scalable and Modular Architecture for CSS)

OOCSS와 BEMS의 발전형이라고도 할 수 있지만 
SMACSS에서는 5가지 성질로 나누어 생각합니다. 

__B=Base____L=Layout____M=Module____S=State(상태)____T=Theme__. Layout에 관해서는 "l-"등의 접두사를 붙이는 것이 권장되고 있습니다. 

BEM와 다른 점은  SMACCS에서는 클래스마다 위의 "하나 하나"의 성격을 갖는다는 규칙이 있습니다.

```html
<div class="l-main">
    <div class="panel is-bordered is-wide"></div>
</div>
```

장점
* 클래스마다 하나의 성질 밖에 가지지 않기 때문에, 각 클래스의 역할이 알기 쉽다.
* OOCSS의 멀티 클래스의 장점과 BEM의 클래스 이름 별 성격 알기 쉬움을 좋은 모습을 가지고.

단점
* 접두사는 SMACSS는 규칙을 모르는 사람이 보면 의미를 알 수 없다.
* Layout만 접두사 포함하는 것이 대단히 기분 나쁜 (개인적으로).

# 명명 규칙의 선택
지금까지 소개한 3개의 명명 규칙은 크게 나누면 두 사상으로 나누어집니다.
단일 클래스 또는 (BEM) 멀티 클래스 또는 (OOCSS, SMACSS). 

선택은 취향이지만 각각 뚜렷한 장점과 단점이 있어 룰을 결정하고 코딩을 추진하고 후회하지 않는 선택을 하고 싶은 곳.
어느 쪽을 선택 하느냐는 취향되지만, 각각 뚜렷한 장단점이 있기 때문에 규칙을 정해 코딩을 추진하고에서 후회없는 선택을하고 싶은 곳.


# 나는 내가 규칙 만들기
내 경우 최근 자 체 규칙을 만들어 사용하는 경우가 많아지고 있습니다.

싱글 클래스는 CSS에서 취급 어렵기 때문에 멀티 클래스 싶습니다.
싱글 클래스는 CSS상에서 다루기 힘든 것으로 멀티 클래스로 하고 싶다.

알기 어려운 접두사는 사용하고 싶지 않다.
기본 -> 확장 개념은 클래스 이름 표한다.
등 개인적인 생각을 바탕으로 BEM의 명명 규칙 알기 쉬움을 살린 채 멀티 클래스를 사용하는 명명 규칙을 생각합니다. 

```html
<div class="main">
    <div class="panel panel--bordered panel--wide"></div>
</div>
```


배너 패널에 기본 스타일 .panel과 확장이다 .panel - bordered를 함께 설정합니다.

BEM 정도로 하나 하나의 클래스 이름이 길지 않으며 CSS도 기본 스타일과 확장 스타일을 솔직하게 쓰고 더해 갈 수 있기 때문에 좀처럼 쓰기 쉬운 것입니다. 

"panel"라는 명칭이 다른 요소에 여러 번 나오는 앉아 행동은 부정 할 수 없지만, BEM의 이름의 복잡성에 비하면 허락 할 것입니다. 


사이트 구조에 따라서는 이 명명 규칙이 빠지지 않는 것도 당연히 있기 때문에, 이 경우에는 그 사이트에 맞추어 규칙을 조정하기로 하고 있습니다. 
규칙에 좌지우지되지 않는다. 나는 (코딩하는 사람)이 규칙 인 것이다.
룰에 휘둘리지 않는다. 나(코딩하는 사람)이 규칙인 것이다.




정리
HTML / CSS 명명 규칙은 어디 까지나 '원칙'으로 일하는 것이므로, 당연히 예외는 나와 버리고 엄격하게 규칙을 따르는 것이 항상 옳다고 할 수 없다고 생각합니다. 

"만들기 쉬움" "가독성" "확장성"등을 균형있게 의식하면서 스스로 기분 좋은 네이밍을 모색합시다. 

결국 최종적으로 가장 중요한 것은 " 쓰고 있고 잘 어울릴지 어떨지"네요!

쓰고 있고 잘 어울릴지 여부
결국 마지막으로 가장 중요한 것은 "쓰고있어서 잘 오는 여부"군요!
결국 최종적으로 가장 중요한 것은 " 쓰고 있고 잘 어울릴지 어떨지"네요!


















