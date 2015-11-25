# team slogup Coding Convention

HTML, CSS에 관한 코딩 스타일 가이드 **for Markup Languages (HTML/CSS)**
>A style guide is about consistency. Consistency with this style guide is important. Consistency within a project is more important. Consistency within one module or function is most important.

>But most importantly: know when to be inconsistent -- sometimes the style guide just doesn't apply. When in doubt, use your best judgment. Look at other examples and decide what looks best. And don't hesitate to ask!    
 
><br />스타일 가이드는 일관성에 관한 것입니다. 이 스타일 가이드의 일관성은 중요합니다. 한 프로젝트에서의 일관성은 더 중요합니다. 한 모듈과 함수에서의 일관성은 훨씬 더 중요합니다.

>그러나 가장 중요한 것은 일관성이 필요없을 때가 언제인지 아는 것입니다 왜냐면, 때때로 스타일 가이드가 적용되지 않을 때가 있기 때문입니다. 의심이 들때에는 당신의 판단을 믿으세요. 다른 예제들을 보시고 어떤 것이 잘 만들었는지 결정하십시오. 그리고 질문 하는것을 주저하지 마세요.  
(인용 출처: [Style Guide for Python Code : PEP 0008](http://www.python.org/dev/peps/pep-0008/#a-foolish-consistency-is-the-hobgoblin-of-little-minds))

## Overview
1. 네이밍 규칙
2. HTML 코드 작성 규칙
3. CSS 코드 작성 규칙
4. 웹접근성
5. 알아두면 좋은 특징들

## 1. 네이밍 규칙
### 1.1 BEM(Block, Element, Modifier)
####1.1.1 개요  
BEM은 Yandex에서 고안된 프론트엔드 네이밍 방법론입니다. team slogup에서 사용하는 BEM은 [Nicolas Gallagher](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)에 의해 다듬어진 것을 토대로합니다.  
  
기본적으로 세가지의 패턴으로 이루어져 있습니다.  
**.block{}**  
**.block__element{}** (쌍아래붙임표)  
**.block--modifier{}** (쌍붙임표)

붙임표들을 홑이 아닌 쌍을 붙인 이유는 block의 이름에 (header-search)가 가능하기 때문입니다. 

####1.1.2 block  
block은 가장 높은 단계의 추상화 또는 컴포넌트입니다.

####1.1.3 block\_\_element  
.block의 하위 자손들입니다. 하지만 DOM적으로 하위 요소라고해서 block\_\_element로 정할 순 없습니다.  
**.header{}**  
**.header__logo{}**  
에서 logo가 .header안에 우연히 있는 요소라면 BEM을 적용하지 않는게 좋습니다. 
**.site-logo{}**  
로 표현하는 것을 추천합니다.

####1.1.4 block--modifier   
.block의 다른 상태와 버전을 나타냅니다.

####1.1.5 예제  

	<div class="media">
    	<img src="logo.png" alt="Foo Corp logo" class="img-rev">
    	<div class="body">
        	<h3 class="alpha">Welcome to Foo Corp</h3>
        	<p class="lede">Foo Corp is the best, seriously!</p>
    	</div>
    </div>
    
위의 예제에서 .media와 .alpha와의 관계성이 있는지 없는지 알 수 없습니다. 그리고 그 외의 요소들도 마찬가지입니다.

	<div class="media">
    	<img src="logo.png" alt="Foo Corp logo" class="media__img--rev">
    		<div class="media__body">
        		<h3 class="alpha">Welcome to Foo Corp</h3>
        		<p class="lede">Foo Corp is the best, seriously!</p>
    	</div>
    </div>

BEM을 적용했을때입니다. .media_img--rev에서 이 요소는 .media의 자식 요소이며 rev가 적용되었다는 것을 알 수 있고 .media와 .alpha는 관련성이 없다는 걸 알 수 있습니다. 


(참조: [MindBEMding – getting your head ’round BEM syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/))

### 1.2 slogupBEMed
####1.2.1 webname
	
	<body>
		<div class="webname">
			<header></header>
			<div class="webname-main"></div>
			<footer></footer>
		</div>
	</body>
	
webname은 사용할 고유 이름이며 프로젝트 이름의 약어를 활용합니다.
다른 모듈과의 중복을 방지하기 위해서 일반적인 단어를 지양합니다.  
  
####1.2.2 모듈과 container
web application내에서 독립된 모듈을 사용할 경우 모듈을 container로 감싸줘야합니다.
container는 web application과 모듈을 한 단계 분리 시킴으로써 모듈에 대한 CSS 스타일링이 쉽도록 해줍니다.

	
	<div class="sectionName wrapper">
        <div class="sectionName__moduleName-container">
        <!--/*Module-->
            <ng-include src="/../../moduleName">
            or
            <div moudleName></div>
        <!--Module*/-->
        </div>
    </div>
    
하지만 위의 예제처럼 모듈이 container의 child만 가능한건 아닙니다. 모듈은 container의 descendant도 가능합니다.
    
    
### 1.3 네이밍 문자
####1.3.1 일반 규칙  
1. 문자와 숫자조합이 가능합니다.
2. 시작문자는 문자만 가능합니다.
3. 두 단어의 조합일 경우 Camel표기법보다는 (-)하이픈을 사용합니다. ex) sectionName -> section-name
4. 단어의 수가 8자 이상일 경우 약어를 사용합니다. 약어를 만드는 규칙은 없습니다. ex) team slog up -> tsg
5. 쌍(아래)붙임표는 약속어이므로 사용을 금지합니다.
 
## 2. HTML 코드 작성 규칙
### 2.1 outline
#### 2.1.1 주요한 태그들
1) Sectioning root  
하나의 독립된 outline을 제공합니다.
해당되는 태그들은 body, blockquote, figure, td, details, dialog, fieldset 입니다.
2) Sectioning content
sectioning content는 HTML 문서를 섹션으로 나누도록 도와줍니다. 섹션과 그 섹션안의 헤더를 이용하여 outline을 만들 수 있게됩니다. article, aside, nav, section

#### 2.1.2 일반 규칙
1) only H1 - 웹페이지내에서 H1은 하나만 갖습니다. SEO 강화를 위해서 H1은 title과 달라야합니다.  
  
2) sectioning content내에 headings(h1~h6)을 정의해줍니다. 하지만 웹페이지에서 보여줄 때 보이면 안되는 경우가 있습니다. 그럴 때는 부트스트랩에서 제공하는 클래스 sr-only를 사용합니다.  
sr-only를 사용하는 이유는 다른 Hidden text방식이 구글의 검색 랭킹과 웹접근성에 영향을 주기 때문입니다.  
([여러 Hidden text방식에 대한 설명](http://stackoverflow.com/questions/5523194/html5-titles-in-sectioning-elements-document-outline-and-seo-implications?rq=1))  
([구글 Quality guidelines](https://support.google.com/webmasters/answer/66353?hl=en))

3) 아래의 홈페이지에서 HTML구조가 맞는 지 확인해야합니다. team slogup에서는 untitled가 없어야합니다. 
[https://gsnedders.html5.org/outliner/](https://gsnedders.html5.org/outliner/)

### 2.2 HTML 유효 검사
w3c의 유효 검사를 통과해야합니다.  
[https://validator.w3.org/](https://validator.w3.org/)


## 3. CSS 코드 작성 규칙
### 3.1 OOCSS (SCSS)
#### 3.1.1 설치 on Mac
SCSS를 설치하기 위해서는 기본적으로 Ruby가 필요합니다. 하지만 운이 좋게도 맥은 기본적으로 Ruby가 깔려져있습니다.
그래서 터미널에서 아주 간단한 아래 명령어만 입력하면 됩니다.
	
	sudo gem install sass

참조: [sass](http://www.sass-lang.com/guide)

### 3.2 일반 규칙

#### 3.2.1 type selector 지양 
type selector(div, h1, span, ul, li 등등)을 사용할 경우 다른 구역에서의 의도치 않은 CSS가 변경될 수 있습니다.
하지만 type selector의 올바른 사용은 생산성을 높게합니다. SCSS에서 중첩이 2개 이하에서 사용할 때에는 신중할 필요가 있습니다.

#### 3.2.2 The "multi-class" pattern

#### 3.2.3 the Pseudo Class Selectors
https://css-tricks.com/pseudo-class-selectors/
#### 3.2.4 the Pseudo Elements
https://css-tricks.com/almanac/selectors/a/after-and-before/
	
### 3.3 Responsive for CSS
#### 3.3.1 metatag
모바일 기기에서 웹페이지를 볼 경우 모바일 기기는 화면이 작기때문에 웹페이지가 화면을 벗어나게 됩니다. 그래서 모바일기기내에서 화면을 다 볼 수 있게 하기 위해서 아래의 메타태그를 추가해줍니다.  
\<meta name="viewport" content="width=device-width, initial-scale=1" />

#### 3.3.2 breakpoint
반응형에서 이미지나 컨텐츠의 크기가 변하게 되는 지점인 breakpoint를 설정해줘야합니다.
이 breakpoint는 보통적으로 스마트폰, 태블릿, PC로 나눠서 생각합니다. 하지만 세부적으로 들어가면 엄청 다양한 크기가 존재하며 가로화면까지 생각했을때는 breakpoint의 값은 [기기별 breakpoints](https://responsivedesign.is/develop/browser-feature-support/media-queries-for-common-device-breakpoints)에서 나온 만큼 다양해집니다.  
그래서 device중심이 아닌 contents중심으로 breakpoint를 정합니다.  
각 서비스별 contents에 맞는 크기가 있습니다. 화면을 작게한 다음에 점점 크기를 늘려나가면서 어디서 contents가 이상해보이는지 확인을 한 후 breakpoint를 정합니다.  
breakpoint는 variables.scss 에서 정의합니다.

#### 3.3.3 mixin
1) mixin 활용  
@mixin media($args...)    
app에서 사용되는 구문  

2) $args... options  
"screen" : "only screen"  
"print" : "only print"  
"retina" : "(-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3/2), (min-device-pixel-ratio: 1.5), (min-resolution: 120dpi)"  
">": "min-width"  
"<": "max-width"  
"desktopWidth": $mediaDesktopWidth   
"tabletWidth": $mediaTabletWidth   
"phoneWidth": $mediaPhoneWidth   
  
3) 사용방법   
적용하고자 하는 CSS Selector의 block안의 맨아래에 @mixin media($args...)을 추가한다.

  
[참고: Dmitry Sheiko](http://codepen.io/dsheiko/pen/KeLGy)
### 3.4 Grid 사용

### 3.5 Mixin
http://nicolasgallagher.com/about-html-semantics-front-end-architecture/

### 3.6 image 
#### 3.6.1 icon
1) icon-font보다는 SVG를 사용합니다.  
[( icon-font vs svg )](https://css-tricks.com/icon-fonts-vs-svg/)    

2) icon이 많을 때는 css sprite를 사용합니다.  
[( Icon System with SVG )](https://css-tricks.com/svg-sprites-use-better-icon-fonts/)  
[An Overview of SVG Sprite Creation Techniques](https://24ways.org/2014/an-overview-of-svg-sprite-creation-techniques/)

## 4. 웹접근성
### 4.1 Skip navigation
### 4.2 Headings

## 5. 알아두면 좋은 특징들
