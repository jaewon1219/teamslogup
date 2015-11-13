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
### 2.1 




## 3. CSS 코드 작성 규칙
### 3.1 OOCSS (SCSS)
#### 3.1.1 설치 on Mac
SCSS를 설치하기 위해서는 기본적으로 Ruby가 필요합니다. 하지만 운이 좋게도 맥은 기본적으로 Ruby가 깔려져있습니다.
그래서 터미널에서 아주 간단한 아래 명령어만 입력하면 됩니다.
	
	sudo gem install sass

참조: [sass](http://www.sass-lang.com/guide)

### 3.2 일반 규칙

#### 3.2.1 type selector 지양 
#### 3.2.2 The "multi-class" pattern
	
### 3.3 Responsive for CSS
### 3.4 Mixin
type selector사용 지양
The “multi-class” pattern
http://nicolasgallagher.com/about-html-semantics-front-end-architecture/

## 4. 웹접근성
### 4.1 Skip navigation
### 4.2 Headings

## 5. 알아두면 좋은 특징들
