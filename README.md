# What is Sass?

Sass는 css 전처리기로 css를 개발 단계에서 더 편리하게 작성하기 위해 사용하는 package이다.  

css 전처리기에는 stylus, less 등이 있는데 우리는 sass에 대해 공부한다.

Sass는 .scss와 .sass 두 가지 문법을 제공하는데 기능적으로는 동일하다. 하지만 .scss가 css와의 호환성이 좋기 때문에 .scss문법을 배워보기로 한다.  

<br>

# 프로젝트 생성

.scss 파일을 사용하기 위해서는 우선 main.scss파일을 만들고, parcel-bundler를 설치한 다음 아래와 같이 작성해보자.

- index.html
```html
<link ref="stylesheet", href="./main.scss"/>
...
<div class="container">
  <h1>Hello SCSS!</h1>
</div>
```
- main.scss
```scss
$color: royalblue;

.container {
  h1 {
    color: $color;
  }
}
```
- 출력형태  
  <p style="color:royalblue;font-size:32px;font-weight:bold;">Hello SCSS!</p>  

parcel-bundler가 sass를 설치해주고, 자동으로 css로 변환한 뒤에 동작시킨다.

## [sassmeister.com](http://sassmeister.com)  
sass로 작성한 문법을 css와 비교하기 간편하다.

<br>

# 주석

Sass는 두 가지 방식의 주석을 제공한다.
- `/* ... */`  
scss를 css로 변환했을 때 사라지지 않는다.
- `// ...`  
scss를 css로 변환했을 때 사라진다.

<br>

# 중첩(Nesting)

scss에서는 기존의 css에서 사용했던 선택자를 더 편리하게 관리할 수 있다.

index.html
```html
<div class="container">
  <ul>
    <li>
      <div class="name">DAEHUN</div>
      <div class="age">23</div>
    </li>
  </ul>
</div>
```
main.scss
```scss
.container {
  ul {
    li {
      font-size: 40px;
      .name {
        color: royalblue;
      }
      .age {
        color: orange
      }
    }
  }
}
```
main.css(compiled)
```css
.container ul li {
  font-size: 40px;
}
.container ul li .name {
  color: royalblue;
}
.container ul li .age {
  color: orange
}
```
상위 선택자를 반복해서 작성하지 않아도 돼서 작성이 편하다.

<br>

# & - 상위 선택자 참조

&(ampersand)기호를 사용하면 상위선택자를 참조할 수 있게 된다.  

main.scss
```scss
.btn {
  position: absolute;
  &.active {
    color: red;
  }
}

.list {
  li {
    &:lastchild {
      margin-right: 0;
    }
  }
}

.fs {
  &-small { font-size: 12px; }
  &-medium { font-size: 14px; }
  &-large { font-size: 16px; }
}
```

main.css(compiled)
```css
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}

.list li:lastchild {
  margin-right: 0;
}

.fs-small {
  font-size: 12px;
}
.fs-medium {
  font-size: 14px;
}
.fs-large {
  font-size: 16px;
}
```

<br>

# 중첩된 속성

Sass에서는 hipen(-) 앞의 단어(namespace)가 같은 속성을 중첩해서 사용할 수 있다. 선택자처럼 사용하되, 뒤에 colon(:)을 붙여 사용한다.  

main.scss
```scss
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

main.css(compiled)
```css
.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 20px;
  padding-right: 30px;
}
```

<br>

# 변수(Variables)

값의 재사용을 위한 변수를 지원한다. `$` 기호를 변수의 앞에 붙여 사용한다.  

main.scss
```scss
$size: 100px; // global

.container {
    position: fixed;
    top: 200px;
    .item {
        width: $size;
        height: $size;
        transform: translateX($size);
    }
}
```

main.css(compiled)
```css
.container {
  position: fixed;
  top: 200px;
}
.container .item {
  width: 100px;
  height: 100px;
  transform: translateX(100px);
}
```

Sass에서 선언된 변수는 유효범위를 가지는데 위처럼 선택자 밖에서 선언된 변수는 전역 변수로, 모든 범위에서 사용할 수 있다. 반면, 선택자 내에서 선언된 변수는 그 선택자 영역 이하에서만 유효하다.  
또 변수는 재할당이 가능한데 재할당된 line 밑에서는 재할당된 값으로 읽힌다. 

<br>

# 산술 연산

css에서는 아래의 기호로 각 연산을 수행한다.
- add(+)
- sub(-)
- mul(*)
- div(/)
- mod(%)  
단, 연산하는 값의 단위는 같아야한다. 다른 단위의 산술연산을 하기 위해서는 `calc()`함수를 이용한다.

## 나머지 연산

css의 단축속성인 font는 세 가지 개별속성을 지정할 수 있는데 font-size와 line-height 속성을 구분하기 위해 slash(/) 기호를 사용한다.
```css
span {
  font-size: 10px;
  line-height: 10px;
  font-family: serif;
  /* same as */
  font: 10px / 10px serif;
}
```

이 때문에 `/` 기호를 바로 사용했을 때는 연산이 제대로 이뤄지지 않는다.  

나머지 연산을 수행하는 방법은 아래와 같다.

1. 괄호로 연산을 묶는 경우  

main.scss
```scss
div {
  margin: (30px / 2);
}
```
main.css(compiled)
```css
div {
  margin: 15px;
}
```

2. 연산할 값을 변수에 할당하는 경우

main.scss
```scss
$size: 30px;
div {
  margin: $size / 2;
}
```
main.css(compiled)
```css
div {
  margin: 15px;
}
```

3. 다른 연산을 수행한 값과 함께 사용하는 경우

main.scss
```scss
$size: 30px;
div {
  margin: 9px + 12px / 2;
}
```
main.css(compiled)
```css
div {
  margin: 15px;
}
```

# 재활용(mixins)

CSS에서는 한 번 사용한 style을 다른 개체에서도 사용하기 위해서 복사와 붙여넣기를 사용했다. Sass에서는 이것을 효과적으로 하기 위해 재활용 기능을 지원한다.  
정의할 때는 `@mixin`, 사용할 때는 `@include`로 사용한다.

main.scss
```scss
@mixin center{
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
```
main.css(compiled)
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container .item {
  display: flex;
  justify-content: center;
  align-items: center;
}
```
Sass는 재사용의 편의를 위해 매개변수의 사용을 지원한다. default 값을 지정하기 위해서는 해당 매개변수의 뒤에 값을 적는다. 또, 매개변수의 할당은 순서에 의존하기 때문에, 첫 번째가 아닌 매개변수를 지정한다면 매개변수의 이름을 명시해야 한다.

main.scss
```scss
@mixin box($size: 100px, $color: tomato) {
    width: $size;
    height: $size;
    background-color: $color;
}
.container {
    @include box(200px);
    .item {
        @include box($color: green);
    }
}
```
main.css(compiled)
```css
.container {
  width: 200px;
  height: 200px;
  background-color: tomato;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: green;
}
```

<br>

# 반복문

Sass에서 반복문은 아래와 같이 사용한다. 보간은 `#{ expr }`과 같이 사용한다( ` 기호 없이 사용).

main.scss
```scss
@for $i from 1 through 10 {
  .box:nth-child(#{$i}) { width: 100px * $i; }
}
```

main.css(compiled)
```css
.box:nth-child(1) { width: 100px; }
.box:nth-child(2) { width: 200px; }
  ...
.box:nth-child(10) { width: 1000px; }
```

<br>

# 함수

mixin도 함수와 비슷한 개념이기는 하지만 mixin은 함수보다는 속성의 모음에 가깝다. Sass는 값을 연산하여 반환하는 함수 기능을 제공한다.

main.scss
```scss
@function ratio($size, $ratio) {
    @return $size * $ratio
}

.box {
    $width: 100px;
    width: $width;
    height: ratio($width, 9/16);
}
```

main.css(compiled)
```css
.box {
  width: 100px;
  height: 56.25px;
}
```

<br>

# 색상 내장 함수

Sass는 전역에서 사용할 수 있는 내장 함수를 제공한다. 

### `mix($color1, $color2)`

두 가지 색상을 입력 받아 두 색상을 혼합(mix)한 색상을 반환한다.


# 색상 내장 함수

Sass는 전역에서 사용할 수 있는 내장 함수를 제공한다. 

### `mix($color1, $color2)`

두 가지 색상을 입력 받아 두 색상을 혼합(mix)한 색상을 반환한다.

### `lighten($color, n%)`, `darken($color, n%)`

`$color`를 `n%` 밝게(lighten) 또는 어둡게(darken)한 색상을 반환한다.

### `saturate($color, n%)`, `desaturate($color, n%)`

`$color`의 채도를 `n%`만큼 높이거나(sturate), 낮춘(desaturate) 색상을 반환한다.

### `grayscale($color)`

`$color`를 회색조로 바꾸어 반환한다.

### `invert($color)`

`$color`를 반전시킨 색상을 반환한다.

### `rgba($color, opacity)`

`$color`에 `opacity` 만큼의 투명도를 적용하여 반환한다. CSS에서 사용하는 `rgba(red, green, blue, opacity)`보다 인수가 적어 쓰기에 편리하다.

<br>

#  가져오기

`@import`를 통해 `url()`없이, 확장자 없이, 다른 scss파일을 연결할 수 있다.

index.html
```html
<div class="container">
	<h1>Hello SCSS!<h1>
</div>
```

main.scss
```scss
@import "./sub";
//만일 가져오려는 파일이 두 개 이상이면 "./sub", "./sub2", ... 로 가져올 수 있다.

$color: royalblue;

.container{
	h1 { color: $color }
}
```

sub.scss
```scss
.container{ background-color: orange; }
```

출력형태
<div style="background-color: orange"><p style="color:royalblue;font-size:32px;font-weight:bold;">Hello CSS!</p></div>

