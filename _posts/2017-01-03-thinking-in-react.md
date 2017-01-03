---
title: Thinking in React.
updated: 2017-01-03 12:00
---
 
# Thinking in React

React는, 우리생각엔, 자바스크립트를 이용한 크고 빠른 웹앱을 만드는 최선책이다. It has scaled very well for us at Facebook and Instagram.

React의 많은 부분중에 가장 훌륭한 부분은, 당신이 앱을 만들때 어떻게 만들지 생각하게 한다는 것입니다.(?) 이 문서에서, React를 사용하여 '검색 가능한 제품 데이터 테이블'을 만드는데 필요한 사고의 과정을 안내합니다.

## 예제랑 시작하기

우리는 JSON API와 예제 디자인을 가지고 있다고 생각해보자. 예제는 이렇게 생겼다.
![sample1](https://facebook.github.io/react/img/blog/thinking-in-react-mock.png)

우리의 JSON API는 아래의 값을 반환한다.

```
[
  {category: "Sporting Goods", price: "$49.99", stocked: true, name: "Football"},
  {category: "Sporting Goods", price: "$9.99", stocked: true, name: "Baseball"},
  {category: "Sporting Goods", price: "$29.99", stocked: false, name: "Basketball"},
  {category: "Electronics", price: "$99.99", stocked: true, name: "iPod Touch"},
  {category: "Electronics", price: "$399.99", stocked: false, name: "iPhone 5"},
  {category: "Electronics", price: "$199.99", stocked: true, name: "Nexus 7"}
];
```

## Step 1: UI를 Comonent 계층으로 나누기

첫번째로 당신이 하고 싶은 일은 예제의 각 Component별로(하위 Component에도) 네모를 치고, 이름을 지어주는 것이다. 만약 니가 디자이너와 협업을 한다면, 걔들이 이미 했을 것이다. 그러니 가서 달라고하세요! 그들의 Photoshop layer이름이 아마 React Component의 이름일 테니 말이다.

그러나 그것이 그것만의 component인지 어떻게 알 수 있을까? 그냥 새로운 함수나 객체를 만들어야 하는지 결정할 때 같은 기술을 사용해라. 앞서 말한 기술 중 하나는 [단일 책임 원칙](https://en.wikipedia.org/wiki/Single_responsibility_principle), 즉 하나의 component는 이상적으로 단 하나의 기능만 하는 것이다. 만약 니가 여기까지 성장 했다면, 더 작은 하위component까지 나눠져야 된다.

당신은 JSON데이터 모델을 유저들에게 보여줄 일이 많으므로, 만약 당신의 모델이 잘 세워 졌다면, 당신의 UI(다시 말해 conponent 구조)와 잘 매핑될 것이다. 이는 UI 및 데이터 모델이 동일한 *정보 아키텍처*를 따르는 경향이 있기 때문입니다. 즉, UI를 구성 요소로 분리하는 작업은 종종 사소한 작업이 된다. 그러므로 정확히 하나의 데이터 모델을 나타내는 component로 분해하십시오.

![componentImage](https://facebook.github.io/react/img/blog/thinking-in-react-components.png)

우리의 예제 앱에서 5개의 components를 볼 수 있다. 우리는 각 component를 대표하는 data에 italicized표시를 했다.

1. FilterableProductTable(오렌지) : 예제의 전체를 포함하고 있다.
2. SearchBar(파랑) : *모든 유저 입력*을 받는다.
3. ProductTable(초록) : 유저 입력에 기반하여 *데이터 집합*을 보여주고 필터링한다.
4. ProductCategoryRow(청록색) : 각 *카테고리*의 제목을 보여준다.
5. ProductRow(빨강) : 각 *제품*의 줄을 보여준다.

만약 당신이 `ProductTable`을 본다면, 테이블의 헤더('Name'과 'Price'라는 라벨을 포함하고 있다)는 자신만의 component가 아니라는 것을 볼 수 있다. 이것은 취향의 문제인데 어느쪽이든 논쟁의 여지가 있다. 이 예시에서는, 저것을 `ProductTable`의 *data colletion*을 랜더링하는 일부라고 판단하여 `ProductTable`의 부분으로 두었다. 그러나 만약 그 헤더가 더 복잡해 진다면(i.e. 만약 우리가 정렬을 위해 affordances을 추가한다면), `ProductTableHeader`라는 component를 가지는게 말이 될 것이다.

이제 우리는 우리의 예제에서 component들을 확인헀으니, 등급별로 재구성해 보자. 간단하다. 예제의 다른 component의 안에 있는 component들은 그 계층의 아래에 존재하면 된다.

* FilterableProductTable
  * SearchBar
  * ProductTable
    * ProductCategoryRow
    * ProductRow


## Step 2: React의 정적 버젼 구축

<iframe height='265' scrolling='no' title='Thinking In React: Step 2' src='//codepen.io/InHyuk/embed/oBvydx/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='http://codepen.io/InHyuk/pen/oBvydx/'>Thinking In React: Step 2</a> by Jung In Hyuk (<a href='http://codepen.io/InHyuk'>@InHyuk</a>) on <a href='http://codepen.io'>CodePen</a>.
</iframe>


이제 component 계층구조를 가졌다. 이제 당신의 앱을 실행해볼 시간이다. 가장 쉬운 방법은 데이터 모델을 가져와 UI 렌더링을 하지만 상호작용이 없는 버젼을 먼저 만드는 것이다. 이렇게 과정을 나누는 것이 가장 좋다. 왜냐하면 정적버젼은 많은 타이핑이 필요하지만 고민이 필요없지만, 상호적 작용을 추가하면 타이핑은 줄지만 생각할 요소가 많아지기 때문이다. 이유를 살펴보자.

데이터 모델을 렌더링하는 당신의 앱을 정적버젼으로 만들기 위해, 당신은 다른 component를 재사용하고 *prop*를 이용해 데이터를 주고받는 component를 만들고 싶을 것이다. *props*는 부모에서 자식으로 데이터를 전달하는 방법이다. 만약 *state*의 개념에 익숙하다면, 정적버젼을 만들때는 **state를 사용하지마라.**  State는 오직 상호작용을 위한 것이다. 즉, 시간에 따라 변하는 값이다. 정적벼젼의 앱을 만드는 동안은 필요하지 않다.

당신은 top-bottom 이나 bottom-top으로 만들 수 있다. 즉, 당신은 계층의 위에서 아래로(i.e. `FiterableProductTable`에서 시작) component를 만들거나 아래에서 위로(i.e. `ProductRow`에서 시작) 만들 수 있다. 간단한 예에서는 top-bottom이 더 쉽고, 보다 큰 프로젝트에서는 bottom-up과 테스트 코드를 함께 진행하는것이 더 쉽다.

이 step의 마지막에서, 당신은 당신의 데이터 모델을 랜더링 하는데 재사용이 가능한 component들의 '도서관'을 가지게 될 것이다. 그 component들은 정적버젼의 앱을 만들 동안에는 오직 `render()`함수만 가지고 있다. 그 component의 최상위 계층(`FilterableProductTable`)은 당신의 데이터 모델을 prop로 가지게 될 것이다. 만약 당신의 기본적인 데이터 모델을 변화시키고 `ReactDOM.render()`을 다시 실행시키면, 당신의 UI는 업데이트 될 것이다. 이것은 복잡한 일이 없기 때문에 UI가 어떻게 업데이트되고 어디에서 변경해야하는지 쉽게 볼 수 있다. React의 **단방향 데이터 흐름(*one-way data flow* 또는 *one-way binding* )**은 모든것을 모듈화 되고 빠른 상태로 유시지켜 준다.

[React docs](https://facebook.github.io/react/docs/hello-world.html)에 당신이 이 단계를 시도해 보는데 필요한 간단히 내용을 적어놨다.

**짧은 막간: Props vs State**
React에는 두가지 타입의 "model" 데이터: 'props'와 'state'가 있다. 두가지의 목적에 대해 이해하는것이 중요하다. 만약 당신이 두가지의 차이점에 대해 확신하지 못하겠다면, [The official React docs](https://facebook.github.io/react/docs/state-and-lifecycle.html)를 훑어봐라.

## Step 3: UI State의 최소한의(그러나 완벽한) 표현 식별
당신의 UI의 상호작용을 만들기 위해서는, 당신의 기반이된 데이터 모델을 수정할 수 있어야 한다. React는 이 것을 state와 함께 쉽게 만들어 준다.

당신의 앱을 올바르게 만들려면, 당신이 첫번째로 필요한 것은 당신의 앱이 필요로 하는 최소한의 변화하는 state집합이다. 간단한 키는 *너 자신을 반복하지 마라*이다.
애플리케이션이 필요로하는 상태를 절대적으로 최소한으로 표현하고 필요에 따라 필요한 모든 것을 계산해라. 예를 들어, 만약 당신이 TODO list를 만든다면, 단지 TODO items의 배열만 유지하면 된다 ;카운트에 대한 별도의 상태를 유지하지마라. 대신, TODO의 갯수를 랜더링할때, TODO items의 배열의 길이를 가져오면 된다.

우리의 예제 앱에서의 모든 데이터 조각을 생각해 보아라. 우리는:
* 제품의 원래 목록
* 유저가 입력한 검색 값
* 체크박스의 값
* 제품의 필더링된 목록

각각 생각해 보고, 어느 것이 State인지 구별해 보자. 각 data 부분들에 관한 간단한 세가지 질문을 해보자.
1. 이것이 부모를 통해 props로 전해져 내려오는가? 그렇다면 아마 state가 아니다.
2. 시간이 지나도 변화가 없는 채로 남아있는가? 그렇다면 아마 state가 아니다.
3. 당신이 당신의 component에서 다른 state나 props를 통해 그 값을 계산해 낼 수 있는가? 그렇다면 아마 state가 아니다.

제품의 원래 목록은 props로 전해져 내려오기 때문에 state가 아니다. 유저가 입력한 검색값과 체크박스는 시간이 지나면 변하고 어떤것으로도 계산해 낼 수 없기 때문에 state인 것처럼 보인다. 그리고 마지막으로 제품의 필터링된 목록은 나머지 위의 3가지로 계산이 가능하므로 state가 아니다.

그래서, 우리의 state는:
* 유저가 입력한 검색 값
* 체크박스의 값

## Step 4: 당신의 state가 어디에 있는지 확인하자

<iframe height='265' scrolling='no' title='Thinking In React: Step 4' src='//codepen.io/lacker/embed/ORzEkG/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='http://codepen.io/lacker/pen/ORzEkG/'>Thinking In React: Step 4</a> by Kevin Lacker (<a href='http://codepen.io/lacker'>@lacker</a>) on <a href='http://codepen.io'>CodePen</a>.
</iframe>

OK, 그래서 우리는 최소한의 앱 state의 집합을 알아냈다. 다음, 어느 component가 이 state를 변화시키거나 주인이 되는지 알아내야 된다.

React는 모든것이 component의 계층적 one-way flow에 관한 것이라는 것을 기억하자. 어느 component가 어느 state의 주인이 되는지 지금은 명확하게 인식되지 않을 수 있다. **이것이 대부분의 초심자가 이해하기 가장 어려운 부분이다.** 그래서 이 단계들을 따라오면서 그것을 밝혀보자:

당신의 앱에서의 각각의 state조각들은:
* 해당 상태를 기반으로 무언가를 렌더링하는 모든 component를 식별한다.
* 공통된 소유자의 component를 찾는다(그 계층에서 state가 필요한 모든 component들의 상위에 존재하는 하나의 component)
* 공통 소유자 또는 계층 구조에서 상위에있는 다른 component는 상태를 소유해야한다.
* state를 소유해야 할 component를 찾지 못하곘다면, 그 state를 소유할 새로운 component를 간단히 만들고 공통 소유자의 component의 계층에 추가해라.

이 전략을 우리의 예제 앱에 적용해 보자:
* `ProductTable`은 state에 따라 제품 목록을 필터링해야하며 `SearchBar`는 검색 값과 선택된 state를 표시해야 한다.
* 그 공통된 소유자의 component는 `FilterableProductTable`이다.
* `FilterableProductTable`에 필터 텍스트와 체크된 값이 저장되는 것이 개념적으로 맞다.

좋아. 우리는 `FilterableProductTable`이 우리의 상태를 가지기로 결정했다. 먼저, `this.state = {filterText: '', inStockOnly: false}`를 `FilterableProductTable`의 `constructor`에 당신의 앱의 state를 초기화 하기위해 추가해라, 다음, `filterText`와 `inStockOnly`를 `ProductTable`과 `SearchBar`에 prop로 넘겨 줘라. 마지막으로, 그 props들을 이용해 `ProductTable`을 필터링 하고 `SearchBar`의 값을 설정해라.

당신은 당신의 앱이 어떻게 움직이는지 확인 할 수 있다: `filterText`에 `"ball"`을 넣으면 당신의 앱이 갱신된다. 당신은 테이터 테이블이 올바르게 업데이트 된 것을 확인할 수 있을 것이다.

## Step 5: 역 데이터 흐름 추가

<iframe height='320' scrolling='no' title='Thinking In React: Step 5' src='//codepen.io/snakajima/embed/JbYQvL/?height=320&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='http://codepen.io/snakajima/pen/JbYQvL/'>Thinking In React: Step 5</a> by Satoshi Nakajima (<a href='http://codepen.io/snakajima'>@snakajima</a>) on <a href='http://codepen.io'>CodePen</a>.
</iframe>

지금까지, 우리는 계층별로 아래로 흐르는 형식의 props와 state의 함수들이 정확하게 랜더링되는 앱을 만들었다. 이제 다른 방향의 데이터 흐름을 지원해 볼 차례이다.
계층 구조의 깊숙한 폼 component는 `FilterableProductTable`에서 상태를 업데이트해야한다.

React는 이 데이터 흐름을 명시적으로 만들어 어떻게 당신의 프로그램이 작동하는지를 쉽게 이해할 수 있게 해준다. 그러나 이것은 이전의 양방향 데이터 바인딩 방식보다 조금 더 많은 타이핑을 요구한다.

만약 당신이 현재 버젼의 예제에서 input에 값을 넣거나 체크박스를 체크하더라도 React는 당신의 input을 무시하는 것을 볼 수 있다. 이것은 의도적으로 우리가 `input`의 `value` prop를 항상 `FilterableProductTable`에서 주는 `state`와 같게 만들었기 때문이다.

우리가 어떤 일이 일어나길 원하는지 생각해보자. 우리는 유저가 언제든지 폼을 바꿀 수 있고, 유저의 input에 따라 state가 반영되길 원한다. component들은 자체 상태 만 업데이트해야하므로, `FilterableProductTable`은 상태를 업데이트해야 할 때마다 실행되는 SearchBar에 콜백을 전달한다. 우리는 input의 `onChange`이벤트를 이용해 그것을 알려줘야 된다. 그리고 `FilterableProductTable`에 의해 전달 받는 콜백은 `setState()`를 호출하고 app은 업데이트 될 것이다.

복잡하게 들리지만, 코드상으로는 몇 줄 되지 않는다. 그리고 어떻게 당신의 대이터가 앱에서 흐르는지가 매우 명확해 진다.

## 그리고 끝
React와 함께 어떻게 component를 만들고 어플리케이션을 만드는지에 대한 아이디어를 얻었길 바란다. 이전보다 조금 더 타이핑 할 수도 있지만, 코드는 작성된 것보다 훨씬 많이 읽혀 지므로, 이 모듈 식의 명시 적 코드가 읽기에 매우 쉽다는 것을 기억해라. 당신이 큰 components의 라이브러리를 만들기 시작할 때, 이 명확함과 모듈화된것과, 코드 재사용으로 코드 줄이 줄어드는 것에 감사할 것이다.:)

