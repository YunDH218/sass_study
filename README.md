# What is Sass?

Sass는 css 전처리기로 css를 개발 단계에서 더 편리하게 작성하기 위해 사용하는 package이다.  

css 전처리기에는 stylus, less 등이 있는데 우리는 sass에 대해 공부한다.

Sass는 .scss와 .sass 두 가지 문법을 제공하는데 기능적으로는 동일하다. 하지만 .scss가 css와의 호환성이 좋기 때문에 .scss문법을 배워보기로 한다.  

<br>

# 프로젝트 생성

.scss 파일을 사용하기 위해서는 우선 main.scss파일을 만들고, parcel-bundler를 설치한 다음 아래와 같이 작성해보자.

index.html
```html
<link ref="stylesheet", href="./main.scss"/>
...
<div class="container">
  <h1>Hello SCSS!</h1>
</div>
```
main.scss
```scss
$color: royalblue;

.container {
  h1 {
    color: $color;
  }
}
```
출력형태  
<p style="color:royalblue;font-size:32px;font-weight:bold;">Hello SCSS!</p>  

parcel-bundler가 sass를 설치해주고, 자동으로 css로 변환한 뒤에 동작시킨다.

## [sassmeister.com](https://sassmeiseter.com)  
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

&(ampersand)기호를 사용하면 상위선택자를 
```
```