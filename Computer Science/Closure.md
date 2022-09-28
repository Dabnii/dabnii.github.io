# <span style="color:orange"> Closure & Lexical & Scope

생소하지만, 알고 보면 우리 가까이에 있던 클로져. <br>
작동원리를 알아보도록 하겠습니다. 

💡 클로져는 스코프, 렉시컬스코프, 렉시컬 환경과 밀접한 관계를 가지고 있습니다.
<br><br>
<hr>
<br>


## 🔭<span style="color:orange"> <strong> Scope | 스코프 </strong> </span>
> - <span style="color:orange"> <strong>유효범위</span></strong>
> - <strong> <span style="color:orange"> 전역스코프, 지역스코프, 전역변수, 지역변수 </strong> 네 가지로 구분
> - 함수가 실행될 때 생성되는 값, 표현식을 찾을때 참고하는 <strong> <span style="color:orange"> '표' </span> </strong>와 유사
> - <span style="color:orange"> 하위 스코프 &#8594; 상위 스코프로만 접근 </span>가능
> - 하나 이상의 스코프가 모인 것을 스코프 체인이라 칭함
> - 함수가 실행 되는 즉시 생성
>    - 함수 단위로 스코프 생성
>   - 모든 변수는 스코프를 가짐

<br>
<br>

## <span style="color:orange"> <strong> 🌎 전역스코프 & 🏠 지역스코프</strong> </span>


&#32;|🌎 전역스코프 Global Scope | 🏠 지역스코프 Local Scope
---|---|---|
선언 위치| <span style="color:orange">블록 { } 바깥 또는 함수 바깥</span>에서 선언 | <span style="color:orange">블록내부</span>에서 선언
사용 가능 범위 | 전역 | 블록 내부 
변수| 🌎 전역변수를 포함<br> Global Variable| 🏠 지역변수를 포함 <br> Local Variable

<br>

    💡 전역 스코프는 전역 변수를 가지며 어디서나 접근 할 수 있습니다.
    지역 스코프는 블록 내부에서 선언되며 선언 된 내부에서만 접근 할 수 있습니다.
<br>
<br>

### 🔭 <span style="color:orange"> 스코프 레벨</span> in JS 
 블록레벨 스코프| 함수레벨 스코프|
---|---
 { } 중괄호, 중괄호 두 개 사이의 범위에서만 존재 <br> <span style="color:orange">let, const | 함수레벨에서 존재 <br><span style="color:orange">var

<br>
<br>

### 🔭 <span style="color:orange"> 상위 스코프의 정의</span> in JS ✨

이름 |정적 스코프  | 동적 스코프 
---|---|---
결정 방식|함수가 <strong><span style="color:orange">정의(선언)</strong>되는 시점| 함수가 <span style="color:orange">호출</span> 되는 시점에 결정
Eng| <span style="color:orange">Lexical scope &#124;&#124; Static scope | Dynamic scope

    함수가 정의(선언) 되는 시점에 정적스코프 (렉시컬 스코프) 또는 동적 스코프로 정의 됩니다. 
<br><br>

## <span style="color:orange"> <strong> 🌎 전역스코프 & 🏠 지역스코프 Sample code_ Fruits </strong> </span>

```java script
const x = 'Apple';  //🌎전역스코프 

function outer() { //🏠지역스코프 
  const x = 'kiwi'; //🏠지역스코프 
  function inner() //🏠지역스코프 
  {
    console.log(x); //🏠지역스코프 
  };
    return inner; //🏠지역스코프 
};
const fruits = outer(); //🌎전역스코프 
fruits(); //🌎전역스코프  // 'kiwi'
```
```java script
fruits() // 'kiwi'
```
<br>

## ✨ 스코프 참조 방향 : <span style="color:orange">하위 &#8594; 상위 &#124;&#124; 내부&#8594;외부
반대의 경우 성립하지 않음 (상위 &#8594; 하위 불가)

상위|전역 스코프|&#32;
---|---|---
&#32;| X | 'Apple'

&#8593; 참조방향


하위|지역 스코프|&#32;
---|---|---
&#32;| X | 'Kiwi'

<br>
🤔 어떻게 전역에 선언된 🍎 'Apple' 아닌 🥝 <strong>'Kiwi' </strong>가 나왔을까요?<br>
outer의 내부 함수인 inner가 전역에 선언된 x = 'Apple'이 아닌 <br>
<span style="color:orange"> 함수 내부에 선언된 x = 'kiwi'값을 지역 스코프에서 참조하였기 때문입니다. <br> </span>
즉 내부 함수에서 값을 찾았기에 전역 함수로 진행하지 않은 것 입니다.<br>
&#32;+ 🤫 전역에서 x를 호출하면 'Apple'이라는 값을 받을 수 있습니다. <br><br>

## <span style="color:orange"> <strong> 🌎 전역스코프 & 🏠 지역스코프 Sample code_outer&inner </strong> </span>

```java script
var x = '나는 전역 X야';

function outer() {
  var y = '나는 outer함수의 지역 y야';
  console.log(x); 
  console.log(y); 

  function inner() {
    var x = '나는 inner함수의 지역 x야';
    console.log(x); 
    console.log(y); 
  }
  inner();
}

outer();
console.log(x);
console.log(y); 
//나는 전역 X야
//나는 outer함수의 지역 y야
// 나는 inner함수의 지역 x야
// 나는 outer함수의 지역 y야
// 나는 전역 X야
//https://www.youtube.com/watch?v=PVYjfrgZhtU

```
전역 스코프|&#32;
---|---
 X | '나는 전역 X야'
  outer | function obj

&#8593; 참조방향


outer 지역 스코프|&#32;
---|---
 Y | '나는 outer 함수의 지역 y야'
inner | function obj

&#8593; 참조방향

inner 지역 스코프|&#32;
---|---
 x | '나는 inner 함수의 지역 y야'

<br>

1. outer() 호출 &#8594; outer 함수 실행
1. outer 함수 y = '나는 outer 함수의 지역 y야' 
1. Outer 함수는 <span style="color:orange">전역 스코프로 접근 &#8594; var x = '나는 전역 x야' 값을 참조
2. inner() 실행 &#8594; x = 'inner함수의 지역x야' 라는 값을 갖게 됨
2. inner 함수내의 y는 없으므로 &#8594;  inner함수의 상위 함수인 outer 함수에 접근
3. inner함수는 outer 함수의 x 값인 <span style="color:orange"> '나는 outer 함수의 지역 y야' 라는 값을 참조 
1. console.log(x)는 전역 스코프만을 참조할 수 있어 '나는 전역 X야' 값을 가짐
1. <span style="color:orange">!!! console.log(y) 값은 undefined . 전역에서 내부 스코프로 진입할 수 없기 때문



<br><br>
<hr>
<br>

## ✍️  <span style="color:orange"> <strong> Lexical Environment | 렉시컬 환경 (어휘점 환경) </strong> </span>
> - 어떠한 코드가 어디에서 실행 되는 등 대체적인  <span style="color:orange">정보를 담고 있는 환경
> - 포함하는 식별자, 식별자에 바인딩 된 값,  <span style="color:orange">상위 렉시컬 환경에 대한 참조를 담은 하나의 자료 구조 
>   - 함수가 실행되는 즉시 Lexical 환경 생성

<br>

``` Javascript
let one;
one = 1;

function addOne(num){
  console.log(one + num);
}

addOne(5); // 6
// https://www.youtube.com/watch?v=tpl2oXQkGZs
```

전역 Lexical 환경|&#32;
---|---
one | 1
addOne | funcion obj

&#8593; 참조방향 (반대의 방향 불가)

내부 Lexical 환경|&#32;
---|---
num | 5 

<br>

## 📌 <span style="color:orange"> <strong> Closure | 클로져 </strong> </span>
> - <span style="color:orange">함수 와 렉시컬 환경의 조합 </span> 입니다. <br>
> -  <span style="color:orange"> 내부 함수가 소멸된 외부 함수에 접근 할 때 <strong> 내부 함수를 클로져 </span> </strong> 라고 합니다.

<br>

    클로져는 소멸한 함수에도 접근 할 수 있음을 뜻합니다. (대부분의 함수는 1회 실행 후 다시 접근할 수 없습니다.)
    외관이 망가진 차량이 있지만 내부의 엔진이 살아 있다면 접근할 수 있는 것과 비유하면 조금 더 이해가 쉬우실 것 같습니다. :)
    함수가 소멸되어도 스코프는 '기억' 되어 접근 할 수 있습니다.
    


<br>
<hr>

## 🙇‍♀️ 마치며


미래의 기술 면접을 위하여 클로저 발표를 준비했습니다.<br>
발표하는 과정에서 멤버들 개인의 언어로 이해한 내용을 공유할 때 확실하게 이해할 수 있는 소중한 경험을 했습니다.<br>
저의 언어로 풀어낸 이 포스팅이 다른 분들께도 도움이 되길 바랍니다!<br>

난이도가 있는 '클로저 은닉화', '클로저 반복문'은 담지 못하였지만 가까운 미래에 다시 업로드 하겠습니다!

3355 화이팅! 늘 좋은 자극을 주어서 감사해요.