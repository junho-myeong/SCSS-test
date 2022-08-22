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



