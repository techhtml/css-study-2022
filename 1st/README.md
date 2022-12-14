# CSS란?
- CSS (Cascading Style Sheet)
- 엑셀 (Spread Sheet), 구글 시트 (Google Sheet)
- Sheet > 데이터가 나열된, 열거된 공간
- Style Sheet > 스타일이 나열된 공간
- 논리적인 결과물을 만들어낼 수 있는 것 X
- Cascading > 폭포
- Cascading 이라는 특성을 지닌 스타일 시트 (= CSS)

- CSS 1.0 > 2.1 > 2.2 > 3.0 > 4.0
- CSS Version은 그렇게 의미가 있지는 X
- 특정한 스타일에 대한 표준이 만들어지고, 그 표준을 관리
- CSS Grid Layout (모듈 단위로 관리)

## 셀렉터 101 (선택자)
- CSS는 스타일의 나열
- 스타일을 어디에 적용할 지?
- > 셀렉터 (Selector)

```html
<article>
  <h1>CSS 스터디</h1>
  <p>이 스터디는 CSS를 배우는 스터디입니다.</p>
  <div>
    <!-- DIV 요소의 자식 요소: P -->
    <!-- ARTICLE 요소의 자손 요소: P -->
    <p>DIV 요소 안에 들어가 있는 P 요소</p>
  </div>
</article>
```

- article 요소에 스타일, h1 요소에 스타일

```css
/* 요소 셀렉터 */
/* 요소 이름을 작성하면 끝 */
article {}
h1 {}
p {}
div {}
```
장점 겸 단점
- 해당 이름의 요소에는 모두 스타일이 적용
- 요소 이름을 바꾸면 적용 X

```css
/* 클래스 셀렉터 */
/* 특정한 클래스명을 가진 요소에 스타일을 부여 */
/* 숫자나 특수문자로 시작하면 X */
/* 클래스명은 기본적으로 중복이 가능 */
.box {}
.area {}
.wrapper {}
.container {}
.header {}
.footer {}
```

```html
<!-- Box 스타일 -->
<div class="box">
  <h1>안녕하세요</h1>
</div>
<!-- Box 스타일 + Area 스타일 -->
<div class="box area">
  <h1>안녕하세요</h1>
</div>
<!-- Box 스타일 + Area 스타일 + Container 스타일 -->
<div class="box area container">
  <h1>안녕하세요</h1>
  <div>
    <h1>안녕하세요</h1>
  </div>
</div>
```

## 콤비네이터 101 (결합자)
- Selector 만으로 못하는 것들
- 특정한 조건에 충족했을 때에만, 자식 요소나 형제 요소를 제어하고 싶을 때
- > Combinator

```css
/* 특정한 요소의 자손 요소에 스타일을 주고싶은 경우 */
/* 자손 콤비네이터 */
/* 공백 문자 */
/* {조상 요소} {자손 요소} */
/* 자식 요소에 관계 없이, 자손 요소 중 해당 요소가 있다면 적용 */
div h1 {}
div p {}
.box h1 {}
.area h1 {}
.area .title {}
```

```html
<ul class="main-menu">
  <li>
    메인 메뉴
    <ul class="sub-menu">
      <li>펼쳐지는 서브 메뉴</li>
      <li>펼쳐지는 서브 메뉴</li>
    </ul>
  </li>
<ul>
```

```css
/* 특정한 요소의 자식 요소에 스타일을 주고싶은 경우 */
/* 자식 콤비네이터 */
/* > */
/* {부모 요소} > {자식 요소} */
.main-menu {}
.main-menu > li {}
.sub-menu {}
.sub-menu > li {}
```

```html
<article>
  <h1>제목</h1>
  <p>설명</p>
  <h2>제목 2</h2>
  <p>설명</p>
</article>
<ul>
  <li>리스트 아이템</li>
  <li>리스트 아이템</li>
  <li>리스트 아이템</li>
  <li>리스트 아이템</li>
</ul>
```
```css
/* 특정한 요소의 형제 요소에 스타일 주고싶은 경우 */
/* 첫째는 형제를 몰라요 */
/* 형제 콤비네이터 */
/* ~ */
/* 특정한 요소의 형제이기만 하면 OK */
/* h1 요소의 형제 요소인 P 요소 전체에 스타일 주고 싶어 */
h1 ~ p {}

/* 인접 형제 콤비네이터 */
/* + */
/* 특정한 요소의 형제인데, 해당 요소에 바로 붙어있는 형제 요소 */
/* h1 요소에 바로 붙어있는 형제 요소인 P 요소에게만 스타일을 주고 싶어 */
h1 + p {}
/* li 요소에 바로 붙어있는 형제 요소인 Li 요소에게만 스타일 */
li + li { border-top: 1px solid #eee }
```

```css
/* 이렇게도 작성할 수 있다. */
/* 이론상 조합에 제한 X */
/* 복잡도가 높을 수록 관리 포인트가 많아지고 힘들어집니다. */
/* 옛날에 17 중첩 */
/* 4 중첩은 안넘어가는 게 좋은 거 같다.. */
.box > div > h1 + p {}
.box ~ .box > h1 {}

/* 셀렉터도 조합 */
div.box {}
.box.area {}
.button.on {} /* variants */
.button.off {} /* variants */
```

## 가상 셀렉터, 가상 요소
- 가상 (psuedo, 의사)
- 코드상으로 개념적으로 존재하는 것들, 가상
- 요소로 완전히 존재하는 건 아니지만, 개념적으로 존재하는 것들
- 특정한 요소에 마우스를 올린 상태

```css
/* 마우스를 올린 상태, 요소에 관심을 준 상태 */
/* 터치 스크린에서는 한번 클릭한 상태 */
a:hover {}

/* 마우스를 클릭한 상태, 요소가 활성화된 상태 */
a:active {}

/* 특정한 링크를 이미 사용한 상태, 이미 방문한 사이트 */
a:visited {}

/* 특정한 요소에 포커스가 간 상태 */
a:focus {}
```

- 가상 요소
- 어떤 스타일을 넣기 위해서 요소를 추가해야하는 데, 이 요소가 의미론적으로는 필요는 없는데... 스타일을 위해 넣어야 돼.
- 아이콘
- 가상 요소를 사용하면, HTML이 존재하는 것처럼 가상으로 요소를 추가
```html
<div>
  <!-- ::before -->
  <span class="text">텍스트</span>
  <!-- ::after -->
</div>
```

```css
/* ::before, ::after */
/* 가상 요소 셀렉터는 모두 :: 를 사용 */
/* content 속성이 필수값 */
/* 별도로 display 속성을 지정하지 않았다면, text로 취급 */
/* 복사 할 때 가상 요소 콘텐츠는 복사 범위 X */
/* 스타일적으로는 필요하나, 의미론적으로는 필요 없을 때 */
div {}
div::before { content: '' } /* div 요소의 앞편 */
div::after { content: '' } /* div 요소의 뒤편 */
input::placeholder {}
```

## 캐스케이딩
```html
<!-- Blue -->
<div class="box area">무슨 색이게?</div>
```

```css
.box {
  color: red;
}

.area {
  color: blue;
}
```
- 스타일이 중복되거나, 여러 스타일을 한 요소에 적용했을 때 어떤 걸 적용할 지
- 폭포
  - 스타일이 어느 위치에 존재하는 지 
    (같은 특정성이라면 뒤쪽에 존재하는 게 적용)
  - 특정성이 높은 순서대로 적용
    - 셀렉터 중 ID 셀렉터의 갯수를 셉니다 (= a)
    - 셀렉터 중 클래스 셀렉터, 속성 셀렉터, 가상 클래스의 갯수를 셉니다 (= b)
    - 셀렉터 중 요소 셀렉터와 가상 요소의 갯수를 셉니다 (= c)
    - 전역 셀렉터는 무시합니다.
    - { a b c }
  - !important 키워드 (안 쓰는 게 좋으니까 있는 것만 알아두세요)
```css
#box { color: red } /* a = 1, 특정성: 100 */
.box { color: blue } /* b = 1, 특정성: 010 */
.area {} /* b = 1, 특정성: 010 */
.box .area {} /* b = 2, 특정성: 020 */
.box.area.container {} /* b = 3, 특정성: 030 */
div {} /* c = 1, 특정성: 001 */
div.box {} /* b = 1, c = 1, 특정성: 011 */
div[lang] {} /* 속성 셀렉터 */
```
## 상속
- 상속
- 부모에 적용된 스타일이 자손 요소까지 영향을 주는 경우
- 다른 요소들에 특별히 CSS로 font-size를 지정하지 않으면, body의 font-size를 기본값으로 가져갑니다.
- 컬러, 폰트, 타이포 같은것들은 대부분 자손 요소에 영향 O

```css
body {
  font-size: 18px;
  line-height: 22px;
  color: #333;
}

/* input 같은 요소는 자체적인 스타일 */
/* inherit 이라는 속성 값을 지정해서 명시적 상속 */
input, button {
  font-size: inherit;
  color: inherit;
}
```

## 스타일 적용법과 각 적용법별 장단점
- 3가지 방법
- 특정한 요소에 `style` 속성을 이용해서 `style` 부여하기
- 장점: 딱 해당 요소에만 스타일이 들어감, 특정성에서 우선순위가 높게
- 장점: 자바스크립트 등을 이용해서 요소별로 다르게 스타일을 줘야 되는 경우 `style` 속성을 사용해서 넣기
- 단점: 그 외 모든 것 (확장성 저하)
```html
<div style="color:red">Red</div>
<div style="background-image:url(${url})">배경 이미지가 있는 박스</div>
```
- `<style>` 요소를 사용해서, 해당 페이지에 스타일을 주는 방법
- 리액트 같은 모던 웹 애플리케이션 개발에서 많이 쓰임
- Styled Component 라는 걸 쓰시면 이 방식으로 동작
- 장점: 페이지별로 필요한 스타일만 지정해서 사용
- 장점: 자바스크립트로 제어하기가 수월 (CSSOM)
- 단점: 공통 스타일을 관리하기에는 어려움
- 단점: 페이지별로 들어가는 거라, 모든 페이지에 공용 X
```html
<head>
  <style>
    .box {}
    .area {}
  </style>
</head>
```
- 외부 파일로 `css` 파일을 만듭니다.
- `<link>` 요소를 사용하여 해당 CSS를 연결
- 장점: 공통으로 쓰이는 스타일을 관리하기 쉽다.
- 단점: 외부에 파일이 있기 때문에, HTTP 요청이 한 번 발생
- 단점: CSS에 대한 이해도가 낮은 상태에서 공통 스타일을 만들면 지옥도가 펼쳐지기 쉽다. => 모든 상황에서 다 그렇긴 함.

```html
<head>
  <link rel="stylesheet" href="style.css" />
</head>
```

## 다음 시간 맛보기 (레이아웃)
