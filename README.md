# sass(Syntactically Awesome Style Sheets)

- set the node-sass
npm install -g node-sass

- compile and save in the dir
node-sass style.scss -o .

- when style.scss is changed, automatically, recompiling 
node-sass style.scss -w -o .



# index

1. Variable (변수)
2. Math Operators (수학 연산자)
3. Built-in Functions (내장함수)
4. Nesting (중첩)
5. Import (불러오기)
6. Extend (상속)
7. Mixin (믹스인)
8. Function (함수)


# 1. Variable (변수)
- sass
```
$primary-color: #333;

body {
  background-color: $primary-color;
}
```
- css
```
body {
  background-color: #333;
}
```

# Variable Scope (변수 범위)

- sass
```
$primary-color: #333;

body {
  $primary-color: #eee;
  background-color: $primary-color;
}

p {
  color: $primary-color;
}
```
- css
```
body {
  background-color: #eee;
}

p {
  color: #333;
}
```

# !default
- !default 플래그는 해당 변수가 설정되지 않았거나 값이 null 일떄 값을 설정.

- sass
```
$primary-color: #333;

$primary-color: $eee !default;

p {
  color: $primary-color;
}
```
- css
```
p {
  color: #333;
}
```

# 2. Math Operators (수학 연산자)

- sass
```
.container { width: 100%; }


article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```
- css
```
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 62.5%;
}

aside[role="complementary"] {
  float: right;
  width: 31.25%;
}
```

# 3. Built-in Functions (내장함수)
- check the more sass functions :
http://sass-lang.com/documentation/Sass/Script/Functions.html

- sass (using darken() method)
```

$buttonColor: #2ecc71;
$buttonDark: darken($buttonColor, 10%);
$buttonDarker: darken($buttonDark, 10%);

button {
  background: $buttonColor;
  border-radius: 3px;
  box-shadow: 0px 5px 0px $buttonDark;
  border: 0;
  color: white;
  font-size: 17px;
  padding: 10px 30px;
  display: inline-block;
  outline: 0;
  &:hover {
    background: $buttonDark;
    box-shadow: 0px 5px 0px $buttonDarker;
  }
  &:active {
    box-shadow: none;
    margin-top: 5px;
  }
}
```

# 4. Nesting (중첩)

- css
```
/* CSS */
.container {
    width: 100%;
}

.container h1 {
    color: red;
}
```

- sass
````
/* Sass */
.container {
    width: 100%;
    h1 {
        color: red;
    }
}
````

# reference parents

- sass
````
a {
  color: black;
  &:hover {
    text-decoration: underline;
    color: gray;
  }
  &:visited {
    color: purple;
  }
}
````

- css
````
a {
  color: black;
}
a:hover {
  text-decoration: underline;
  color: gray;
}
a:visited {
  color: purple;
}
````

# 5. Import (불러오기) 

- @import directive (you can use both)
````
@import "layout.scss";
@import "layout";
````

# partial

- 만약에 .sass 파일이나 .scss 파일의 파일이름을 underscore _ 로 시작하면 css 파일로 따로 컴파일되지 않습니다.
  
  html 에서 해당 css 파일을 불러올일이 없고, import 만 되는경우에는이 기능을 사용하세요.
  
# 6. Extend (상속) 

- sass
````
.box {
  border: 1px solid gray;
  padding: 10px;
  display: inline-block;
}

.success-box {
  @extend .box;
  border: 1px solid green;
}
````

- css
````
.box, .success-box {
  border: 1px solid gray;
  padding: 10px;
  display: inline-block;
}

.success-box {
  border: 1px solid green;
}
````

# Placeholder

- Placeholder 선택자 % 를 사용하면 상속은 할 수 있지만 해당 선택자는 컴파일되지 않음.

- sass
````
%box {
  padding: 0.5em;

}

.success-box {
  @extend %box;
  color: green;
}

.error-box {
  @extend %box;
  color: red;
}
````

- css
````
.success-box, .error-box {
  padding: 0.5em;
}

.success-box {
  color: green;
}

.error-box {
  color: red;
}
````

# 7. Mixin (믹스인)

- you should use both @mixin directive and @include directive

- sass
````
@mixin headline ($color, $size) {
  color: $color;
  font-size: $size;
}

h1 {
  @include headline(green, 12px);
}
````

- css
````
h1 {
  color: green;
  font-size: 12px;
}
````

# applied media query

- #{ } 표현은 특정 문자열을 따로 처리하지않고 그대로 출력 할 때 사용됩니다.
  
- @content directive 를 사용하면 나중에 @include 하였을 때, 그 선택자 내부의 내용들이 @conent 부분에 나타나게됩니다.
 
 - sass
 ````
@mixin media($queryString){
    @media #{$queryString} {
      @content;
    }
}

.container {
    width: 900px;
    @include media("(max-width: 767px)"){
        width: 100%;
    }
}
 ````
 
 - css
 ````
.container {
  width: 900px;
}
@media (max-width: 767px) {
  .container {
    width: 100%;
  }
}
 ````


# Function (함수)

- use @function directive
 
 - sass
 ````
@function calc-percent($target, $container) {
  @return ($target / $container) * 100%;
}

@function cp($target, $container) {
  @return calc-percent($target, $container);
}

.my-module {
  width: calc-percent(650px, 1000px);
}
 ````
 
 - css
 ````
.my-module {
  width: 65%;
}
 ````


# Refrences
https://velopert.com
