# SCSS-test

## SCSS(CSS Preprocessor)란?
- CSS가 동작하기 전에 사용하는 기능으로,
웹에서는 분명 CSS가 동작하지만 우리는 CSS의 불편함을 이런 확장 기능으로 상쇄할 수 있습니다.
- 불필요한 선택자(Selector)의 과용과 연산 기능의 한계, 구문(Statement)의 부재 등 프로젝트의 규모가 커질수록 아쉬움도 같이 커지죠.
하지만 웹에서는 표준 CSS만 동작할 수 있기 때문에 다른 선택권이 없습니다.
- 웹 브라우저에서는 CSS만이 작동하기 때문에 SCSS로 작성된 언어를 CSS로 바꿔주는 컴파일을 해줘야 한다.
- 그 컴파일을 해주는것은 npm parcel bundler가 우리의 프로젝트에 SCSS가 연결 되어 잇다면, 자동으로 패키지를 설치하여 컴파일을 진행함으로써 우리는 CSS를 좀더 편리하게 사용할수 잇게 되는것이다

## 주석
- /\*~~~\*/ - SCSS를 CSS로 컴파일 했을때는 CSS에서도 그 코드가 남아 잇다
- // - SCSS로 CSS로 컴파일 했을때 CSS에서는 주석 처리 부분이 사라지는것이다.

## 중첩 with SassMeister
- 상위 선택자를 반복해서 작성할 필요가 없다라는 장점을 가지고 잇다.
``` SCSS
.container {
  // SCSS에서 제공해주는 중첩이라는 기능이다.
  > ul { // container에 바로 자식 요소라는 것을 나타내는것이다.
    li {
      .name {
        color: $color;
        /*font-size: 60px;*/
        //background-color: orange;
      }
      .age {

      }
    }
  }
}
```

## 상위(부모) 선택자 참조
- &(중첩된 선택자의 영역에 상위 선택자를 참조한다.)
```SCSS
// SCSS
.btn {
    position: absolute;
    &.active {
        color: red;
    }
}

.list {
    li {
        &:last:childe {
            margin-right: 0;
        }
    }
}
```
``` CSS
/* CSS */
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}

.list li:last:childe {
  margin-right: 0;
}
```

## 중첩된 속성
- 단축 속성과 관련된 속성에서 자주 사용한다.
- 네임스페이스가 동일하다는것을 뜻한다(font처럼 이름 부분이 동일한 부분)
``` SCSS
.box {
    font: {
        weight: bold;
        size: 10px;
        family: sans-serif;
    };
    margin: {
        top: 10px;
        left: 20px;
    };
    padding: {
        top: 10px;
        bottom: 40px;
        left: 20px;
        right: 30px;
    };
}
```

## 변수
- 변수의 유효 범위가 잇다. 변수를 중괄호 밖에 선언하면, 전역 변수로 사용하고
- 선택자 안에서 사용하게 되면, 그 중괄호 내부가 유효 범위가 된다.
- 값에 재할당도 가능하다, 범위가 동일하다면 재할당된 후에 바뀐 값이 적용이 된다.
- $size: 100px;

``` SCSS
$size: 200px;
.container {
    position:fixed;
    top: $size;
    .item {
        width: $size;
        height: $size;
        transform: translateX($size);
    }
}
```

## 산술연산
- 기본적으로 단위가 동일해야한다.
- 그래서 이렇게 단위가 다를때는 calc함수를 통해서 연산을 해주면 된다.
``` SCSS
div {
    width: 20px + 20px;
    height: 40px - 10px;
    font-size : 10px * 2;
    margin: 30px / 2;
    padding: 20px % 7;
}

div {
    width: 20px + 20px;
    height: 40px - 10px;
    font-size : 10px * 2;
    margin: (30px / 2);
    padding: 20px % 7;
}
// 나누기 연산자를 사용할때 단축속성으로 사용되느것을 막아 줘야한다.
span {
    $size: 100px;
    font-size: 10px;
    line-height: 10px;
    // 폰트 관련 단축속성은 font라는 단축 속성이 가능하다. 앞 폰트 사이트, 뒤에는 line-height
    // 단축속성을 사용할때는 / 기호로 구분해서 사용하기 때문에 산술연산으로 받아 들이지 못한다.
    // () 소괄호를 통해서 사용한다.
    // 변수를 사용해서 나누기를 한다.
    // 다른 연산자와 같이 사용한다.
    font: 10px / 10px; 
    margin: $size / 2;
    padding: 10px + 2px / 2;
}
```

## 재활용(mixin)
- 예를들어 가운데 정렬을 하는 코드를 재활용 할수 잇다.
- 변수와 유사하다.
```SCSS
@mixin center {
    display: flex;
    justify-content: center;
    align-items: center;
}
.container {
    @include center;
    .item {
        @include center;
    }
}
.box {
    @include center;
}
// 재활용을 할때 인수를 통해서 같은 구조를 가진 코드에서 그 값을 다르게 사용할수도 잇다.
// JS에서 함수를 선언하고 호출하는것과 똑같은 방법이다.
@mixin box($size: 100px, $color: tomato) { // 기존에 100px이 기본값이 라면 : 을 통해서 지정해 둘수 잇다.
    width: $size;
    height: $size;
    background-color: $color;
}

.container {
    @include box(200px, red);
    .item {
        @include box($color: green); // 기본적으로 매개변수의 순서에 따라서 그값이 할당 되는데, 기본값은 그대로 두고 싶다면 키워드 인수를 사용한다.
    }
}

.box {
    @include box;
}
```

## 반복문
``` SCSS
// for(let i = 0; i < 10; i++) {
//     console.log('test')
// }

// 오버워치 프로젝트에서 캐릭터 이미지를 삽입 할때 사용하면 편하게 사용할수 잇다.
@for $i from 1 through 10 {
    // 제로 베이스가 아니다.
    // 보관법을 사용해서 변수를 사용할수 잇는데 JS와 다르게 #으로 보관법을 사용한다.
    .box:nth-child(#{$i}) {
        width: 100px * $i;
    }
}
```

## 함수
``` SCSS
// CSS에 속성과 값을 재활용 하는 용도로 사용할때는 mixin을 사용하고
@mixin center {
    display: flex;
    justify-content: center;
    align-items: center;
}

// 실제로 값을 따로 연산해서 반환된 결과로 사용할때 사용한다.
@function ratio($size, $ratio) {
    @return $size * $ratio
}

.box {
    $width: 100px;
    width: $width;
    height: ratio($width, 9/16);
    @include center;
}
```

## 색상 내장함수
``` SCSS
.box {
 $color: red;
 width: 200px;
 height: 100px;
 margin: 20px;
 border-radius: 10px;
 background-color: $color;
 &.built-in {
     // 색상을 섞어 새로운 색상을 리턴 해주는 함수이다.
     background: mix($color, royalblue);
     // 색상을 10퍼센트만큼 밝게 해준다.(hover효과에서 많이 사용한다.)
     background: lighten($color, 10%);
     // 색상을 어둡게 해준다.(hover에서 효과를 줄때 많이 사용한다.)
     background: darken($color, 10%);
     // 채도를 더 높여 준다.
     background: saturate($color, 10%);
     // 색상에 채도를 낮춰준다.
     background: desaturate($color, 10%);
     // 주어진 색상을 회색으로 만들어 준다.
     background: grayscale($color);
     // 생삭을 반전 시켜준다.
     background: invert($color);
     // rgba(색상에서 투명도를 추가해준다.)
     background: rgba($color, .5);
 }
}
```

## 가져오기
- @import 에서 url함수를 따로 사용하지 않고 경로만 지정해도 된다.
- 확장자 또한 표현해 주지 않아도 된다.
- 쉽표로 구분해서 여러개의 파일을 가져 올수도 잇다.
``` SCSS
@import "./sub", "/sub2";

$color: royalblue;

.container {
  h1 {
    color: $color;
  }
}
```
## overwatch project refactoring

## 데이터종류
``` SCSS
$number: 1; // .5, 100px, 1em
$string: bold; // relative, "../images/a.png"
$color: red; // blue, #ffff00, rgba(0,0,0,.1) - 색상 데이터이다, 문자 데이터가 아니다.
$boolean: true; //false
$null: null;
$list: orange, royalblue, yellow; //JS에 배열과 비슷하게 ,로 구분해서 순서대로 사용하는것
$map: ( //JS에서 객체 데이터와 유사하게 key,value 형태로 구성한다.
    o:orange,
    r:royalblue,
    y:yellow
)

.box {
    width: 100px; //number 타입
    color: red; // color 타입
    position: relative; // string 타입
}
```
## 반복문 @each
``` SCSS
$list: orange, royalblue, yellow; //JS에 배열과 비슷하게 ,로 구분해서 순서대로 사용하는것
$map: ( //JS에서 객체 데이터와 유사하게 key,value 형태로 구성한다.
    o:orange,
    r:royalblue,
    y:yellow
);

@each $c in $list {
    .box {
        color: $c;
    }
}

@each $key, $value in $map {
    .box-#{$key} {
        color: $value;
    }
}
```

## 재활용@content
``` SCSS
@mixin left-top {
    position: absolute;
    top: 0;
    left: 0;
    // mixin을 사용할때 기본적인 사항에 특이한 사항을 추가해야하는경우에는 content를 사용해서 
    // 밑에서 추가적인 내용을 더해서 사용할수 잇게 해준다.
    @content;
}

.container {
    width: 100px;
    height: 100px;
    @include left-top;
}

.box {
    width: 200px;
    height: 300px;
    @include left-top {
        bottom: 0;
        right: 0;
        margin: auto;
    }
}
```



