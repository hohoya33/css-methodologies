CSS 방법론 (OOCSS, BEM, SMACSS)


참고
http://wikibootup.org/post/css-co-work/#fn:1

styled-components: 요즘 인기있는 컴포넌트 스타일링 방식 중 하나인, JS 코드 내부에서 스타일을 정의하는 방식입니다.

CSS Module: 모듈화된 CSS 로서, CSS 클래스를 만들면 자동으로 고유적인 클래스네임을 만들어서 스코프를 지역적으로 제한하는 방식입니다.

DRY Pattern : 반복되는 코드를 효율적으로 자동화하는 패턴.
코드를 간결하게 유지함으로써 유지보수시에 이점이 있다.




개별적인 CSS 방법론에 빠져보기 전에 
오랜 시간 동안 무엇이 CSS의 유지관리를 어렵게 했는지 알아보는게 좋겠습니다. 

가장 중요한 문제점은 CSS의 전역적 환경입니다. 
우리가 정의하는 모든 스타일은 전역적으로 적용 됩니다. 페이지의 모든 부분에 말이죠.

이 때문에 자세한 이름 짓기 규정으로 유일한 클래스 이름들을 유지하거나 어떤 스타일이 어느 주어진 요소에든 적용되도록 특이성 규칙을 갖고 언쟁을 벌여야 하는 것이 일이 되어버립니다. 

CSS 방법론들은 커다란 코드베이스 위에서 이와 같은 고통들을 피할 수 있도록 CSS를 작성하는 조직법을 제공합니다. 

자 대충 연대기 순으로 인기있는 방법론 몇가지를 살펴보도록 합시다.


# OOCSS
OOCSS (Object Oriented CSS)는 2009년 처음 선보인 방법론으로 두개의 큰 원칙 하에 구성되었습니다. 

## 구조와 겉모습을 분리시킨다 입니다. 
이것은 (레이아웃과 같은) 구조를 정의하는 CSS와 (색깔, 폰트 등) 겉모습을 정의하는 CSS를 뒤섞어 작성해서는 안된다는 것입니다.
이를 통해 어플리케이션에 겉모습을 다시 입히는 일이 쉬워집니다. 

## 원칙은 컨테이너와 내용을 분리하자는 것입니다. 
이것은 요소를 재사용 가능한 객체로 생각함을 의미합니다. 
이 중심 아이디어로 객체가 페이지내 어디있던 상관 없이 똑같이 보이게 됩니다.

OOCSS는 잘 설명 된 가이드라인을 제공합니다. 
그러나 세부적인 접근에 대해서는 그닥 올바른 관점을 제시하지 못합니다. 
SMACSS와 같은 후속의 접근법들이 이 핵심 컨셉을 차용하고 좀 더 자세한 사항을 추가하여 시작하기에 쉽도록 만들었습니다.

# SMACSS
SMACSS (Scalable and Modular Architecture for CSS)는 2011년 소개된 방법론으로 5개의 구분된 카테고리로 CSS를 작성하라 말합니다. 

5개의 카테고리는 베이스 규칙, 레이아웃 규칙, 모듈, 상태(state) 규칙, 테마 규칙을 말합니다. 

SMACSS 방법론은 또한 몇가지 명명법(naming convention)을 추천하고 있습니다. 

레이아웃 규칙에 대해, 반드시 클래스 이름 앞에 꼭 l- 접두어를 붙이거나 layout- 접두어를 붙이라고 말합니다. 

상태 규칙에 대해서는 상태를 기술하는 접두어를 클래스 이름이 붙이라고 말합니다. is-hidden이나 is-collapsed와 같이 말입니다.

SMACSS는 OOCSS와 비교해 그 접근법에 있어 많은 명세를 갖고 있습니다. 
그러나 마찬가지로 어떤 CSS 규칙이 어떤 카테고리에 속하는지 결정하는데에 숙고를 요구합니다. 
이 후에 등장한 BEM과 같은 접근법은 이 결정법중 몇가지를 차용했습니다. 
더 쉽게 적용이 가능 하도록 말이죠.


# BEM
BEM (Block, Element, Modifier)은 2010년에 사용자 인터페이스를 독립된 블록으로 나누는 아이디어를 중심으로 구성되는 방법론으로써 소개되었습니다. 

블록(block)이란 재사용 가능한 컴포넌트를 말합니다(예로 검색 폼을 다음과 같이 정의 합니다. <form class="search-form"></form>). 

요소(Element)는 블록 보다 작으며 블록의 부분이고 그것 자체로는 재사용 할 수 없습니다(예로 검색 폼 안에 있는 버튼을 다음과 같이 정의 합니다. <button class="search-form__button">Search</button>). 

모디파이어(Modifier, 수식어)는 블록이나 요소의 겉모습, 상태, 행위등을 정의하는 엔티티(entity, 개체)를 말합니다(예로 사용불가 상태의 검색 폼 버튼을 다음과 같이 정의 합니다. <button class="search-form__button search-form__button--disabled">Search</button>).

BEM 방법론은 쉽게 이해하기 쉽습니다. BEM의 구체적인 명명법은 입문자들이 복잡한 결정 없이 적용할 수 있습니다. 
그러나 몇몇 불안한 점이 있는데 클래스 이름이 상당히 지저분해 지고 시멘틱 클래스 이름 짓기의 전통적인 명명 규칙을 따르지 않는다는 것입니다. 

이 다음의 접근법인 Atomic CSS 같은 것은 이러한 비 전통적인 방식을 완전히 다른 수준에서 차용 합니다.


# Atomic CSS
(Functional CSS 라는 이름으로도 익숙한) Atomic CSS는 2014년에 도입되었으며 단일 목적을 갖는 작은 클래스를 시각적 기능을 바탕으로 한 이름을 붙여 만드다는 아이디어를 중심으로 구성된 방법론 입니다. 

이 접근법은 OOCSS, SMACSS, BEM의 완전한 대척점에 있습니다-페이지 위의 요소를 재사용 가능한 객체로 다루는 대신 Atomic CSS는 이런 객체지향적 관점을 모두 무시하고 각 요소들을 스타일링하는 재사용 가능한 단일 목적의 유틸리티 클래스를 사용합니다. 

따라서 
<button class="search-form__button">Search</button> 
이렇게 쓰는 대신, 
<button class="f6 br3 ph3 pv2 white bg-purple hover-bg-light-purple">Search</button> 
이렇게 씁니다.

이 예시를 처음 보고 공포심에 흠칫 했다면, 네 여러분은 혼자가 아닙니다-많은 사람들이 이 방법론을 보고 기존 CSS 모범 사례에 대한 위반이라 여겼습니다. 

그러나 여러 다른 시나리오에서 이 모범 사례라는 것이 유효한지에 대한 의문으로 다수의 훌륭한 토론이 있었습니다. 

이 아티클에서 전통적인 관심사 분리는 (심지어는 BEM 방법론을 사용할 때에도) HTML에 의존적인 CSS를 만드는 반면, 아토믹(atomic) 또는 펑셔널(functional) 접근법은 CSS에 의존하는 HTML을 만듦을 잘 보여주고 있습니다. 

양쪽 모두 틀린것은 아닙니다. 
다만 이 면밀한 조사에서 CSS와 HTML의 진정한 관심사 분리는 영원히 달성될 수 없음을 보여줍니다.

CSS in JS와 같은 다른 CSS 방법론은 실제로 CSS와 HTML이 언제나 서로에게 의존적임을 받아들입니다. 
가장 논란이 치열할 방법론들중 하나로 이끕니다.


# CSS in JS
CSS in JS는 2014년 소개되었습니다. 
이 방법론은 CSS 스타일을 별도의 스타일 시트에 정의하지 않고 개개의 컴포넌트에 직접 넣는 방식으로 구성됩니다. 

이 방식은 React JavaScript 프레임웍을 위한 접근법으로 도입되었습니다(React는 이미 별도의 HTML 파일 대신 JavaScript에서 직접 HTML 컴포넌트를 구성하는 방식으로 논란이 되었습니다). 
(역주: 엄밀히 말하면 React는 프레임워크가 아니라 라이브러리입니다.) 

원래 이 방법론은 인라인 스타일을 사용했었습니다. 그러나 이후의 구현에서 JavaScript로 (컴포넌트의 유일한 클래스 이름을 바탕으로 하는)CSS를 생성하고 이것을 문서의 스타일 태그에 넣는 방식을 취하게 되었습니다.

CSS in JS 방법론은 다시 한번 관심사 분리라는 CSS 모범 사례에 정면으로 부딪혔습니다. 웹을 사용하는 방식이 시간이 흐름에 따라 극적으로 바뀌어 왔기 때문입니다. 본디 웹은 대부분 정적인 웹 사이트로 이루어져 있었습니다-여기서 HTML 콘텐트를 CSS 표현으로부터 분리함이 큰 설득력을 가졌습니다. 요즘에는 웹이 동적 웹 어플리케이션을 만드는데 사용됩니다-여기서 재사용 가능한 컴포넌트로 분리하자는 말이 유의미해 집니다.

CSS in JS 방법론의 목표는 컴포넌트를 캡슐화 된 HTML/CSS/JS로 구성하여 견고한 경계로 감쌀 수 있도록 정의하는데에 있습니다. 이런 컴포넌트 내의 CSS는 다른 컴포넌트들에게 영향을 끼칠 수 없습니다. React는 견고한 경계의 컴포넌트를 밀어준 최초의 대중적인 프레임워크 중 하나이며 Angular, Ember, Vue.js와 같은 다른 주류 프레임워크 많은 영향을 끼쳤습니다. 

CSS in JS 방법론이 비교적 새로운 것이며, 웹 어플리케이션 컴포넌트의 시대에 개발자가 CSS에 대한 새로운 모법 사례를 확립하기 위하여 많은 실험이 이뤄지고 있음을 알아 두는게 중요합니다.


수많은 방법론에 압도당하기 쉽지만 완벽한 하나의 접근법은 존재하지 않다는걸 알아두세요
특정한 CSS 코드베이스의 복잡성을 타개하기 위해 취사 선택 할 수 있는 도구들로 여겨주시길 바랍니다. 

작업에 있어 선호에 따라 숙고하여 옵션을 선택하는 일과 최근 이 업계에서 일어난 실험들이 모든 개발자들에게 장기적으로 도움이 될 것입니다!





# 배경

현재 작업하고 있는 웹 뷰(web view)는 크게 세가지 이슈

## 일관적이지 않은 코드 구조
* 작성 규칙이 통일되지 않았다
* 동일 요소에 대한 중복 설정이 많아진다


## 높은 결합도
* 표현(css), 행위(js), 텍스트(html) 간에 명확한 분리가 이루어지지 않았다
* 뷰의 일부 요소가 전체 요소 및 행위(js)에 영향을 미치고 있다
* 스타일 적용 깊이 및 선택자 덮어쓰기도 html 구조를 바꾸기 어렵게 한다


결과적으로 이러한 이슈들은 공동 작업을 어렵게 한다. 
개발 관점 뿐 아니라, 디자인 관점에서도 뷰 테스트를 하기가 어렵다.
작업 시간을 늘릴 뿐 아니라, 작성자들은 뷰를 변화시키는 데에 소극적인 자세를 취하게 된다. 


이런 문제가 있으므로 이것은 개선해야할 사항이다. 
이상적인 개선 목표는 다음과 같다. 


레이아웃 구성과 요소를 결정하는 것은 온전히 디자인 관점에서 가능하고, 
구현은 온전히 개발 관점에서 가능하도록(관점이지 디자이너, 개발자와 같이 사람 단위로 나누는 것은 아니다) 뷰를 구현하는 것이다. 

하지만 당장의 현실적인 고민은 다음과 같다.

- '내'가 만드려는|수정하려는 뷰에 필요한 스타일을 어떻게 쉽게 찾을 수 있을까?
- '내'가 만든 스타일의 의도를 '동료'가 어떻게 하면 쉽게 이해할 수 있을까?


이에 대한 답은 당연히 뷰를 잘 작성하는 것이다. 
하지만 어떻게 그것이 가능할 것인지를 생각해보아야 한다. 
지금이 바로 일관된 방법, 체계적인 방법들이 있었으면 좋겠다고 생각하게 되는 순간이다.


# CSS 방법론

CSS의 역할이 커지면서 CSS를 보다 효율적으로 작성하는 여러가지 아이디어들이 생겼다. 
SMACSS=5형제, BEM=네이밍, OOCSS=재사용

이를 위해 대부분 CSS 선택자로 아이디와 타입(태그)을 사용하지 말 것을 권장한다.

아이디는 재사용이 불가능한 요소이고, 태그에 스타일을 매기면 마크업이 수정될 경우 스타일도 다시 손봐야 하기 때문이다(의존적)

쉬운 유지보수
코드의 재사용
확장 가능
직관적인 네이밍

일관된 방법, 체계적인 방법, 이런게 정리되면 그게 바로 방법론이 된다. 
모듈성, 확장성, 유지보수성을 고려한 설계 방법들을 제안하고 있다. 

* OOCSS
* SMACSS
* BEM

해석이 다를 수 있지만, 셋 다 어렵지 않다. 그럼에도 방법론들을 세개나 알아보는 것에는 거부감이 들지도 모르겠다. 
이렇게 여러개 알아볼 필요 없이 하나만 선택해서 쓰면 되는 것 아니냐는 생각이 들 수 있다. 
하지만 각 방법론들은 서로에게 영감을 주는 관계이므로 하나씩 이해해볼 필요가 있다. 그리고 마지막에 각 방법론에서 쓰이는 방법들이 서로 어떻게 연결되는지 생각해보려고 한다.



# OOCSS (Object Oriented CSS)


BEM이 역할-요소-상태 순으로 정리한다면, 
OOCSS는 구조와 스타일을 분리한다.

중복되는 디자인 요소를 따로 빼내어 반복적으로 사용한다. (공통 스타일 추상화)
컨테이너와 콘텐츠를 분리하고 위치에 의존적인 스타일을 정의하지 않는다.
코드 재사용성이 높아져 코드량이 줄고 성능이 향상되며 유지보수성도 높아지는 장점이 있다.
반면, 마크업에서 동일한 클래스를 여러 곳에 사용하므로 코드가 지저분해지는 단점이 있다.

이 단점을 보완한 것이 OOSass로, 마크업의 복잡함을 프리프로세서 내에서 대신 처리한다.
코드의 재사용량을 증가시키고, 궁극적으로는 더 빠르고 효과적인 스타일시트를 만들어 내는 것입니다
객체 지향 스타일 가이드를 제시한 방법론

## 표현과 구조의 분리

중복되는 스타일을 모듈화 했을 때, 재사용량이 늘어나고 어떠한 엘리먼트에도 적용 가능하기 때문에 같은 결과물을 만들어 냅니다. 

 모든 엘리먼트는 클래스명을 사용하였으며 공통 스타일은 재사용이 가능한 'skin'으로 선언해서 불필요한 중복을 피했습니다.

CSS를 Positioning / Styling으로 객체화하여 Mix & Match 
```css
.position {
    position: relative;
    display: block;
    float: none;
}
.style {
    background: transparent;
    border: none;
}
```
## 컨테이너와 콘텐츠의 분리
DOM 위치에 의존하지 않고 객체의 재사용이 가능한 클래스 기반 모듈 구축

장점
코드의 재사용성이 높아진다.

단점
다중클래스를 사용하여 HTML이 복잡해진다.
의미 있는 클래스 이름을 짓기 어렵다.


## OOSass
OOCSS를 토대로 Sass에 적용하는 방법론

( Less, Sass와 같은 CSS 전처리기를 사용하여 OOCSS의 단점을 보완하고 Mixin을 사용하여 코드의 재활용성과 의미 있는 네이밍 등의 장점을 극대화하여 사용)
http://zerobase.hatenablog.com/entry/2013/02/28/224515

http://takazudo.github.io/blog/entry/2012-12-10-oocsssass.html
http://takazudo.github.io/presentation-oocss-sass/




객체지향 CSS라는 이름이 붙어있지만 클래스나 상속 같은 개념이 포함된 일반적인 의미의 객체지향은 아니다. 

그보다는 결합도 낮추기(decoupling), 
단일 책임의 원칙(single responsibility principle), 
캡슐화(encapsulation)를 강조하는 방법론이다.

oocss는 스타일의 특징(feature)에 따라 범주를 분리하여 구조적으로 선택자들을 적용할 수 있게한다. 이를 위한 두가지 원칙은 다음과 같다.

## 컨테이너(container)와 내용물(content)은 분리
* Not OOCSS style
```css
h3.content-title {
    font-size: @;
}
```
```html
<h3 class="content-title">
the content-title style is location-dependent in h3 tag.
</h3>
```

* OOCSS style
```css
.content-title {
    ...
}
```
```html
<h3 class="content-title">
the content-title style has not a coupling with h3 tag.
</h3>

<span class="content-title">
the content-title style has also not a coupling with span tag.
</span>
```



## 구조(structure)와 표면(skin)은 분리
* Not OOCSS style
```css
.mixed {
    background-color: @;
    font-color: @;
    border: @;
    border-radius: @;
    width: @;
}
```

* OOCSS style
```css
.structure {
    border: @;
    border-radius: @;
    width: @;
}

.skin {
    background-color: @;
    font-color: @;
}
```





첫번째, ‘컨테이너(container)와 내용물(content)은 분리되어야 한다‘부터 살펴보자. 
여기서의 컨테이너, 내용물은 css class에서 흔히 사용하는 의미가 아니다. 
흔히 사용하는 의미가 아니라는 뜻은 ‘margin, border과 같이 레이아웃의 골격’을 컨테이너라 칭하지 않는다는 뜻이다. 
여기서 컨테이너란 스타일의 적용 범위를 제한하는(구체화하는) 범주를 말한다. 반면, 내용물이란 컨테이너로 인해 제한된 스타일의 범주를 말한다. 이렇게 나누는 목적은 스타일 적용 깊이를 가능한 한 줄이는( SMACSS에서도 강조하는 부분 ) 데에 있다.

두번째, 구조(structure)와 표면(skin)은 분리되어야 한다는 그럼 무엇을 의미하는 걸까? 여기서 구조란 중복되는 스타일 요소들의 모음이다. 그리고 표면이란 구조가 아닌 부분, 즉 공통된 특징(feature)이 없는 특정 스타일 요소의 모음이다. 이건 붕어빵 기계와 붕어빵의 차이와 비슷하다. 
붕어빵 기계(structure)는 모양이 바뀌지 않는다. 
하지만 빵(skin)은 자유롭게 바꿀 수 있다. 
빵의 색을 바꿀 수도 있고, 
속에 넣는 것도 팥이나 크림이나 슈크림 등 다를 수 있다. 

디자인에서 예를 들자면 레이아웃이 있다. 레이아웃은 구조의 범주에 속할 수 있다. 실용적인 예로는 뷰의 버튼이 있다.
특정 용도를 가진 버튼(btn)의 넓이(width)가 모두 200px인 경우, 
넓이는 구조라는 범주로 판단해 따로 뺄 수 있다. 
또 다른 예로는 회원가입과 로그인 위젯처럼 비슷한 요소에 대해서 표면은 다르지만(같아도 되고) 동일한 구조를 적용할 수 있다. 결과적으로 두번째 원칙의 목적은 재사용, 유지보수에 있다.

여기까지 읽고 의문이 들 수 있다. 컨테이너(container)와 내용물(content)을 분리한다고 했는데, 적용 깊이가 깊으면 스타일이 쓰이는 뷰와 위치는 명확히 파악이 가능해서 좋지 않은가? 맞는 말이다. 

하지만 그 경우 특정 html에 특화되어 재사용성이 떨어지게 된다. 
즉, 중복 코드를 늘리게 되어 DRY 위반이다. 
사실 css 파일이 개념적으로 잘 분리되어 있다면 적용 깊이를 늘리지 않고도 각 스타일의 목적을 파악이 가능할 것이다.



# SMACSS (Scalable and Modular Architecture for CSS)

* CSS에 대한 확장형 모듈식 구조(by Jonathan Snook)
* CSS의 프레임워크가 아닌 하나의 스타일 가이드

## 사용목적
* Class명을 통한 예측
* 재사용
* 쉬운 유지보수
* 확장 가능

## 유의사항
* 파생된 CSS 셀렉터 사용금지
* ID 셀렉터 사용금지
* !important 사용 금지
* Class 이름은 의미있게, 다른 개발자가 이해할 수 있도록 선언


## SMACSS의 핵심은 범주화이다. (5개 범주로 분류)
Categories  Rough Summary
Base    HTML 요소에 직접 적용하는 스타일
Layout  섹션 단위의 스타일(header, footer)
Module  모델 단위의 스타일(추상화, 재사용 목적)
State   상태 변화를 표현하는 스타일
Theme   뷰 전반에 영향을 미치는 스타일


모듈Module과 테마Theme가 다소 추상적으로 느껴질 수 있으니 넘겨짚고 가자. 
먼저 모듈의 관점에서 ‘모델 단위’는 컴포넌트 단위와 같은 의미
테마에서 ‘뷰 전반에 영향을 끼친다’는 말은 이것이 배경색과 같은 페이지 전반에 적용되는 스타일이라는 것이다. 

### Base - 요소 선택자(element selector)에 적용하는 스타일
기본 스타일(Reset, Default)
```css
body,p,h1,h2,h3,h4,h5,h6,ul,ol,li,dl,dt,dd,table,th,td,form,fieldset,legend,input,
textarea,button,select{margin:0;padding:0}
body,input,textarea,select,button,table{font-size:14px;line-height:1.25}
body.s,.s input,.s textarea,.s select,.s button,.s table{font-family:helvetica}
body{position:relative;background-color:#fff;color:#000}
body.s{-ms-text-size-adjust:none;-webkit-text-size-adjust:none}
img,fieldset{border:0}
ul,ol{list-style:none}
table{border-collapse:collapse}
em,address{font-style:normal}
a{color:inherit;text-decoration:none}
```

### 디렉토리 구조
./app.scss
./_base.scss
./layout/
./layout/main/
./layout/main/_header.scss
./layout/minor/_nav.scss
./modules/
./modules/_button.scss
./theme/

### Layout - 레이아웃과 관련된 스타일 정의
주요(major) 컴포넌트: 머리말header, 꼬리말footer, 내용content
부수(minor) 컴포넌트: 주요 컴포넌트 내에 있는 컴포넌트 (내비게이션 바, 아이템 목록, 폼(회원가입, 로그인, …))
클래스 명 접두사(prefix)로 l-, layout- 등의 명시 요구

```css
#content {
  width: 80%;
  float: left;
}

#aside {
  width: 20%
}

.l-fixed #content {
  width: 600px;
  margin-right: 10px;
}
 
.l-fixed #aside {
  width: 200px
}
```

### Module(Components) - 스타일 재사용을 위한 요소
Block, Element, Module
재사용을 위해 id 셀렉터와 element를 사용하지 않는다.
만약, element 셀렉터를 사용해야 한다면, .box > span 처럼 child 셀렉터를 사용
예시) nav bar, 이미지 슬라이더, dialogs, widgets, tables, icons



### State - 요소의 상태를 나타내는 스타일
* hidden, expend, active, hover 등의 상태에서 사용
* 접두사(prefix)로 is- 등을 명시 is-hidden, is-collapsed
* 자바스크립트 의존성을 가짐 동적인 변화가 가능
* 반면 모듈은 렌더링 시점에 적용되어 정적임

```html
<div class="btn_area">
  <a href="#" class="btn btn_good is-active">좋아요버튼</a>
  <a href="#" class="btn btn_bad">나빠요버튼</a>
</div>
```

```css
.btn {
  display: inline-block;
  background:#ddd;
  border-radius:4px;
}
 
.btn.is-active{
  background:#43f837;
}
 
.btn.is-hidden {
  display: none;
}
```

### Theme - 서비스 전체적인 표현을 결정 (배경, 색, 글꼴, Border)
색상이나 이미지를 불변하는 스타일과 분리
기존 스타일을 재선언하여 사용할 수 있다.
다른 범주(베이스, 레이아웃, 모듈, 상태)를 덮어쓸 수 있음
theme- 등의 접두어를 명시 또는 theme/과 같은 디렉토리로 계층 분리

```css
.mod {
    border: 1px solid;
}

.mod {
    border-color:blue
}
```



위의 요약 설명에 따르면 베이스의 스타일을 모든 하위 모듈들이 공유하게 되는데, 만약 베이스 스타일을 수정하고 싶다면 어떻게 해야 할까? 

원래 베이스는 하나의 목적(용도)을 가진다. 
그러므로 베이스 요소를 다른 목적으로 사용해야 한다면 덮어쓰기(overriding)는 피하는 것이 좋다. 

대신 베이스 요소에 적용할 분리된 모듈을 새로 설계하여 적용해볼 수 있다. 
예를 들어, css 스타일 깊이를 table > tr > td 대신 .module tr > td를 이용해볼 수 있다.



내가 생각하는 SMACSS의 주요내용 이렇다.

하나의 사이트에서 공통으로 적용되는 Base가 되는 css의 집합을 만든다.
예) reset.css

css 이름은 콘텐츠와 직접적으로 연관되고, 이름만으로 어떤 콘텐츠인지 알 수 있도록 해야 한다.

– 접두사를 사용하여 레이아웃, 모듈, 상태 여부를 알 수 있도록 : layout-, module-, is-
– layout-fixed, module-pop, module-login 등

마크업시 재사용이 가능하도록 Id보다는 class로 설정한다.

기능단위로 묶어서 css를 작성한다.
– 특히 반응형 웹 적용시 mediaquery 해상도에 따라 파일을 나누거나 하는 경우가 많은데, 이는 유지보수 및 공동작업 시 혼란(?) 혹은 번거로움을 야기한다.

따라서 기능단위로 그룹화하여 mediaquery 까지 묶어서 작성한다.
– class가 추가되는 경우에는 해당 그룹에 추가하면 된다.

Theme 관련해서는 color등 변경되는 class만 모아서 파일로 관리하면 Theme 생성, 업데이트가 용이할 것임.
– 기본 Theme에 나중에 작성한 css파일이 덮어쓰기 되는 형식


# BEM (Block Element Modifier)


웹페이지를 컴포넌트들의 조합으로 바라보고 접근한 방법론 
SMACSS가 지키면 좋은 가이드라인이라면, BEM은 지켜야 하는 규칙(rule)

BEM은 id 사용을 불허하고, 요소에 직접 스타일을 적용하는 것도 불허한다. 
또한 .sel1.sel2 {..}와 같은 자손 선택자를 피할 것을 강력히 권고

이렇게 규칙이 엄격한 데에는 이유가 있다. 
그것은 위의 OOCSS, SMACSS에서 봤듯이 모두 CSS 공동 작업의 일관성과 재사용성을 위한 것이다. 

BEM이 컴포넌트를 분리하는 범주는 블록, 엘리먼트, 변형자(modifier)
그 중에서도 블록은 BEM에서 중요한 부분이다. 
BEM 문서에도 설명하고 있듯이 BEM의 핵심은 독립된 블록이다 (the key feature of BEM is block’s independence). 
독립적인 기능을 가지는 재사용 가능한(reusable) 컴포넌트가 곧 블록이다. 
한편, 네이밍 측면에서는 네임스페이스의 기능을 한다.

block-name--modifier-name
block-name__element-name


블록은 내부에 또 다른 블록을 적용할 수는 있지만(구조적으로 중첩 구조가 가능하나) 스타일 적용 깊이는 독립적이어야 한다. 
다르게 말해 자손 또는 자식 관계여서는 안된다.

한편, 엘리먼트는 컴포넌트의 부분적 요소이다. 
즉, 블록에 종속되어 재사용 불가능한 스타일 모음이다. 
이와 다르게 변형자는 behavior(js)에 의해 실시간(runtime)으로 변화 가능한 부분이다. 
예를 들어, --hidden, --visible, --pressed와 같이 접미사로 네이밍을 줄 수 있다.

BEM은 선택자에 대해 크게 세가지를 권고한다. 
첫 째, selector의 깊이는 최소화(가능하면 평평하게, be flattened)할 것, 
둘 째, 선택자는 하나의 기능에 충실할 것(하나는 하나만 해라), 
셋 째, 결합도를 줄일 것.

### Block
block은 문단 전체에 적용된 element 또는 element를 담고 있는 컨테이너를 말한다.
ex) logo / login form / menu / search from / content / footer

### Element
element는 block 안에서 특정 기능을 수행하는 컴포넌트이다. 
element는 상황에 따라 달라진다.
각 element는 두 개의 밑줄표시로 연결하여 block 다음에 작성한다.
```css
.header__logo { … }
.header__menu { … }
.header__search { … }
.header__login { … }
```

block 이름이나 element 이름이 길 경우 – 하이픈으로 연결한다.
.block-name__element-name

### Modifiers
block 또는 element의 속성이다
이 속성은 block 또는 element의 외관이나 상태를 변화

Class명은 “–“를 추가하여 modifier 추가

.block--modifier {…}
.block__element--modifier {…}

.block--modifier {…}
.block__element--modifier {…}

탭 메뉴가 다른 영역에서 다른 스타일로 사용된다면,
메인 속성을 복사하여 추가 하거나,
전 처리 장치인 sass의 @extend를 활용하여 속성을 상속 받을 수 있다

.header__navigation { 
      background: #008cba; 
      padding: 1px 0; 
      margin: 2px 0; 
}     
.header__navigation--secondary { 
      @extend .header__navigation;
      
      background: #dfe0e0; 
 }              
.header__navigation { 
      background: #008cba; 
      padding: 1px 0; 
      margin: 2px 0; 
}     
.header__navigation--secondary { 
      @extend .header__navigation;
      
      background: #dfe0e0; 
 }         

class명이 길어진다.
class명은 구체적이고 명료하여 HTML안에서도 읽기 쉬워야 한다
class명이 무엇을 나타내는지 분명하게 전달돼야 한다


* 화면에 보여질 블록(block)을 기준으로 첫번째 순서의 네이밍을 작성한다.
* 그 다음에 블록 안의 요소(elements)들을 "__"으로 연결해서 네이밍을 작성한다.
* 그 다음에 수식어(모양이나 상태)를 "–"으로 연결한 뒤 네이밍을 작성한다.

* 수식어는 boolean이나 key-value 형태로 넣을 수 있다. (-disable, -color-red)
* 예를 들면 .header__logo 또는 .form__button–disabled과 같은 식이다.

* 클래스명이 용도와 형태를 의미하므로 직관적인 것이 장점, 길고 복잡해지는 것이 단점이다.



http://www.risewill.co.jp/blog/archives/5652

CSS설계는 매우 중요한 것입니다.

일정한 규칙이 없으면 
각자가 다른 사고 방식에서 스타일 정의 하고 불필요한 CSS가 늘어나거나 
본인이 아니면 모르는 규칙이 발생해 유지보수 하기 어렵게 되어 버립니다.


그래서 다음을 의식하고 CSS 설계를 실시하는 것이 중요합니다.

직관적인 네이밍
코드의 재사용
쉬운 유지보수
확장 가능




## class 이름의 기본 규칙
* 알기 쉬운 영어 기반의 이름을 붙인다
너무 당연해하지만보고 난 그 요소의 성질이 전혀 상상할 수없는 이름은 NG. 
예를 들어 조금씩 장식의 다른 요소에 .block-1, .block-2, ...와 숫자를 흔들며 나가는 방식이라고 나중에봤을 때 혼란합니다. 

.block-noborder 라든지 .block-red 든가, 각각의 장식의 특징을 알 수있는 이름을 붙이는 것이다. 또 기본적으로는 이름은 영어로 붙인 것이 무난합니다. 

"통상 업무"에 대한 섹션에 이름을 넣으려고했을 때, .tsujogyomu인지 .tsujyogyomu인지 .tsujogyomu인지를 모르기 때문에 싫어한다는 것이 자신에게 이유입니다. 
영어라면 철자가 고유하게 결정테니까.

* 이름 통일감
명명하는 이라기보다는 설계 사상의 이야기입니다 

비슷한 성격을 가진은 이름에 어떤 연결을 갖게 싶은 곳입니다. 
예를 들어 카드 풍의 디자인이 여러 페이지에 존재하는 경우에 어떤 디자인이든 어느 클래스 이름에도 "card"라는 단어가 등장하는 것이 자연 스럽습니다. 

또 하이픈"-"언더파 스코어"_"은 다른 것으로써 혼재될 경우 반드시 취급의 차이를 명확히 합시다.


디자인 변경을 내다보고 명명한다

위의 요소에
.foo-alpha로 명명하면서 디자인 변경으로
.foo-beta의 아래로 이동이 되어 버렸다.
이 또한 있다. 
후출시 디자인 변경은 그만!라고 말하고 싶지 않을 수도 있지만 자신이 편안하기 때문에 일어날 것 같은 디자인 변경을 내다본 명명을 하는 것도 현자의 지혜입니다. 
개요의 요소에는 foo-summary, 본문에는. foo-content,는 식으로 요소의 본질을 대충 표현한 명명을 하면 다소의 디자인 변경에는 견딜 수 있는 HTML이 됩니다. 
사스 테나 부루 디자인이란 놈입니다.


* 디자인 변경을 내다보고 명명한다

왼쪽의 요소에. foo-left로 명명하면서 디자인 변경으로. foo-right과 좌우가 바뀌고 말았다.
위의 요소에. foo-alpha로 명명하면서 디자인 변경으로. foo-beta의 아래로 이동이 되어 버렸다.


후 내 디자인 변경은 그만! 라고 말하고 싶어 될지도 모르지만 자신이 편하게하기 위해 일어날 것 같은 디자인 변경을 예측 한 이름을 두는 것도 현명한 사람의 지혜입니다. 

개요의 요소에는 .foo-summary 본문에는 .foo-content, 등등 식으로 요소의 본질을 대충 표현한 명명을 하면 약간의 디자인 변경은 견딜 HTML됩니다. 



BEM이 유명하지만 요즘은 BEM을 확장한 규칙도 자주 봅니다. 각각의 규칙에 대해서 장점/단점도 소개하겠습니다.




# OOCSS

OOCSS사이트의 예를 들어 이 페이지를 보면 div의 class속성에 size1of3이라고 size2of3라는 것이 사용되고 있는 것을 알 수 있습니다.

살짝 OOCSS를 본 사람 중에는
아 OOCSS는 편리하게 클래스를 많이 붙여주는 스타일을 말하네.

OOCSS는 페이지의 부품을 "모듈"이라는 단위로 나누어 생각하여 사이트의 유지 보수 및 성능 향상 아이디어 중 하나입니다.

그리고 복잡한 부품은이 모듈에 대해 다른 프로그래밍 언어의 클래스 상속의 개념을 이용하여 효율적으로 확장 해 나가는 ... 는 것이 OOCSS의 키모되는 부분이다, 나는 파악하고 있습니다. 그 실현 방법으로 class 속성에 여러 클래스를 맞히는 방식을 취 ...라는 것입니다.

그것을 간단한 모듈을 제작하면서 살펴 보도록합니다.



하하하, 시맨틱 최고 지요
같은 CSS를 복사붙여넣기 해서 사용 하다니..

하지만 의미는 중요하지? 
클래스 이름에 의미를 갖게 할 것?

그러나 이 CSS는 비슷한 버튼이 추가 되었을때 같은 CSS를 복사  

이 2개의 코드는 말하자면, 흑이냐 백이냐라는 이분법적 코드입니다. 

유연성을 추구하면 전자는 뭐 그건 유연하고 있는 것에는 틀림 없지만, 그것, CSS의 뜻은 무엇인가요?
라고 되고 후자는 HTML로는 이상적이지만, CSS 안은 큰일되어 버립니다.

OOCSS를 사용



기본 모듈은 btnbase 클래스가 표현하는 것. 여기에는 버튼의 일반적인 스타일이 적용 
더욱 구체적인 변화는 twitter, facebook같은 같은 스킨으로 클래스에 적용하는 형태

이것이 프로그래밍 언어의 "클래스 상속"같은 느낌으로 Objected Oriented CSS로 명명 된 것 같습니다. 

이것이라면 CSS에 낭비가 없네요. 유사한 버튼이 나타나더라도 btnbase googleplus라는 클래스를 대고 스타일이 적용되도록 만들면 되니깐..


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
구성 요소의 모양은 여전히   위치와 무관합니다.


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

* 더 많은 의미론적 HTML과 CSS
* 특정 HTML 구조에 대한 의존성 감소





---
https://www.monster-dive.com/blog/web_creative/20170525_000315.php




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






