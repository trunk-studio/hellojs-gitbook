## SASS/SCSS

#### SASS 是一種 CSS 加強版的語言，通常稱為預處理器 (preprocessor)，提供很多 CSS 沒有的功能

- SASS
- SCSS

#### 瀏覽器看不懂 SASS / SCSS 需要被 Compile 成為 CSS 之後，瀏覽器才能讀取

#### SASS

```
.header
  heigtht: 80px
  .logo
    position: relative
    a
      display: block
      &:hover
        color: red
  .menu
    width: 500px
```

### 變數功能

#### 原本

```
#item{
  color: #FF00FF;
  text-align: center;
}
.box{
  color: #FF00FF;
  heigtht: 50px;
  width: 60px;
}
input[type="text"]{
  color: #FF00FF;
  border-radius: 7px;
}
h3{
  color: #FF00FF;
  margin: 5px;
}
```

#### 相等於

```
$test-color:#FF00FF;

#item{
  color: $test-color;
  text-align: center;
}
.box{
  color: $test-color;
  heigtht: 50px;
  width: 60px;
}
input[type="text"]{
  color: $test-color;
  border-radius: 7px;
}
h3{
  color: $test-color;
  margin: 5px;
}
```

### 算術

#### 原本

```
.font-big {
  font-size: 19.2px;
}
.font-middle {
  font-size: 13px;
}
.font-small {
  font-size: 5.33333px;
}
```

#### 相等於

```
$font-size: 16px;
.font-big {
  font-size: $font-size * 1.2;
}
.font-middle {
  font-size: $font-size - 3px;
}
.font-small {
  font-size: $font-size / 3;
}
```

### 巢狀結構

#### 原本

```
#box {
  color: #FF00FF;
  text-align: center;
}
#box > .item {
  margin: 10px;
}
#box > .item.active {
  color: red;
}
```

#### 相等於

```
$test-color: #FF00FF;
#box {
  color: $test-color;
  text-align: center;

  & > .item {
    margin: 10px;

    &.active {
      color: red;
    }
  }
}
```

### import

```
@import "global/global.scss";
@import "global/animation.scss";
@import "vendor/vendor.scss";
@import "components/components.scss";
@import "./site/layouts/layouts.scss";
```

### mixin

#### 原本

```
#box {
  background-color: red;
  border: 1px solid #DDD;
  font-size: 20px;
}
#box2 {
  background-color: red;
  border: 1px solid #DDD;
  text-align: center;
}
```

#### 相等於

```
@mixin red-border-box {
  background-color: red;
  border: 1px solid #DDD;
}
#box {
  @include red-border-box;
  font-size: 20px;
}
#box2 {
  @include red-border-box;
  text-align: center;
}
```

### mixin media query

#### 原本要一個一個設置

```
@media (min-width: 1200px) {
  #header {
    width: 985px;
    margin-left: -502px;
    padding-left: 15px;
    padding-right: 15px;
    left: 50%;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  #header {
    padding: 2em 4.5%;
  }
}
@media (max-width: 991px) {
  #header {
    text-align: center;
  }
}
```

#### 現在可以先設置mixin

```
$xs-min-width: 480px;
$sm-min-width: 768px;
$md-min-width: 992px;
$lg-min-width: 1200px;

@mixin xs {
  @media (max-width: #{$sm-min-width - 1px}) {
    @content;
  }
}
@mixin sm {
  @media (min-width: #{$sm-min-width}) and (max-width: #{$md-min-width - 1px}) {
    @content;
  }
}
@mixin sm-min {
  @media (min-width: #{$sm-min-width}) {
    @content;
  }
}
@mixin sm-max {
  @media (max-width: #{$md-min-width - 1px}){
    @content;
  }
}
```

#### 然後用include方式

```
#header {
  @include lg {
    width: 985px;
    margin-left: -502px;
    padding-left: 15px;
    padding-right: 15px;
    left: 50%;
  }
}
#header {
  @include md {
    padding: 2em 4.5%;
  }
}
#header {
  @include sm-max {
    text-align: center;
  }
}
```
