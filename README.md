CSS방법론 (BEM, OOCSS, SMACSS)

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

















