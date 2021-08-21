## checkList

### Q1. CSS를 HTML에 적용하는 세 가지 방법의 장단점은 무엇인가요?
#### - Inline Style Sheet
  HTML 태그의 style 속성에 CSS 코드를 넣는 방법
  ```
  <p style="color: blue">example</p>
  ```
  [장점] 직관적 사용 가능<br>
  [단점] 꾸미는데 한계가 있고, 재사용이 불가능함

#### - Internal Style Sheet
  HTML 문서 안의 `<style>`과 `</style>` 안에 CSS 코드를 넣는 방법
  ```
  <style>
  h1{
    color: blue;
  }
  </style>
  ```
  [장점] HTML 문서 안의 여러 요소를 한번에 꾸밀 수 있음, 한 문서에만 해당되는 스타일 지정 가능<br>
  [단점] 다른 HTML 문서에는 적용할 수 없음, HTML 문서마다 스타일을 매번 지정

#### - Linking Style Sheet
  별도의 CSS 파일을 만들고 HTML 문서와 연결하는 방법
  ```
  h1{
    color: red;
  }
  ```
  적용을 원하는 HTML 문서에 다음 코드 추가
  ```
  <link rel="stylesheet" href="style.css">
  ```
  [장점] 여러 HTML 문서에 적용 가능, 웹의 전체 스타일을 일관성있게 유지하며 변경시에도 일괄적으로 변경되어 효율을 극대화 가능<br>
  [단점] 권장하는 방식으로 전체 페이지를 잘 구조화하여 재사용이 가능한 style을 고려해야 함

### Q2. 여러 개의 CSS 규칙이 한 개의 대상에 적용될 때, 어떤 규칙이 우선순위를 가지게 되나요?
  한 요소에 여러 CSS 규칙이 적용될 수 있는데, 우선순위에 따라 규칙을 결정<br>
  예를들어 브라우저가 각 요소에 기본 규칙을 할당한 상태에서 한 요소에 대해 개발자가 다른 규칙을 지정하면 그 요소는 개발자가 지정한 규칙으로 지정됨<br>
  <br>우선순위는 다음과 같이 적용<br>
  1. 속성 값 뒤에 `!important` 붙임
  2. HTML에서 `[style]` 직접 지정
  3. `#id` 로 지정
  4. `.클래스` `:추상클래스` 로 지정
  5. `태그 이름` 으로 지정
  6. 상위 객체에 의해 상속된 
  `!important > 인라인 스타일 속성 > 아이디 선택자 > 클래스/속성/가상 선택자 > 태그 선택자 > 전체 선택자 `
  
### Q3. 어떤 박스가 `position: absolute;` 인 속성을 갖는다면, 그 위치의 기준점은 어디가 되나요?
#### position
  `position` 프로퍼티는 요소의 위치를 정의하는 개념으로 top, bottom, left, right 와 함께 사용<br>
  `absolute` 는 절대 위치를 나타냄. 기본적으로 화면의 좌측상단을 기준으로 거리를 계산, 만약 부모요소가 있을 시 부모를 기준으로 위치<br>

### Q4. 가로나 세로로 여러 개의 박스가 공간을 채우되, 그 중 한 개의 박스만 가변적인 크기를 가지고 나머지 박스는 고정된 크기를 갖게 하려면 어떻게 해야할까요?
  가변 영역 + 고정 영역으로 나누기<br>
  가변 영역 class = "main", 고정 영역 class = "side"<br>
  1. `<float + negative margin>`
     ```
     .main{
            float: left;
            width: 100%;
            margin-right: -300px;
            padding-right: 300px;
            box-sizing: border-box;
     }
     .side{
            float: right;
            width: 300px;
     }
     ```
  2. `<float + calc method>`
     ```
     .main{
            float: left;
            width: -webkit-calc (100 % -300px);
            width: calc(100 % -300px);
     }
     .side{
            float: right;
            width: 300px;
     }
     ```
  3. `<Table>`
     ```
     .main,
     .side{
            display: table-cell;
            vertical-align: top;
            text-align: left;
     }
     .side{
            width: 300px;
     }
     ```
  4. `<Flex Box>`
      ```
     .main{
            -webkit-flex: 1;
            flex: 1;
     }
     .side{
            width: 300px;
     }
     ```
### Q5. `float` 속성은 왜 좋지 않을까요?
  `float` 는 블록 요소를 정렬하는 속성<br>
  HTML 요소 `div`를 옆으로 나란히 배열하기 위해 `div`에 `float`을 적용하여 한 줄에 배열하도록 적용한다.<br>
  사용방법은 아주 간단한데, 주의할 점이 있다. => 영역분리<br>
  뒤에 따라오는 요소도 나란히 배열되기 때문에 부모 요소에 `overflow: hidden`로 설정을 하면 영역분리가 가능하다.<br>
  또한, 바로 따라오는 요소에 `clear: both`를 추가함으로써 해결 가능하다.<br>
  이처럼 `float`를 이용한 레이아웃을 작성할 때, 부모 요소가 자식 요소의 크기를 반영하지 못하는 문제 발생 => 문서의 흐름에서 제외되어 둥둥 떠다니게 됨
  
### Q6. Flexbox(Flexible box)와 CSS Grid의 차이와 장단점은 무엇일까요?
  웹 레이아웃에 가장 많이 사용되어지는 것은 `Flex`, `Grid`<br>
  `Flex`는 1차원적으로 수평, 수직 영역 중 하나의 방향으로만 레이아웃 나눔<br>
  `Grid`는 2차원적으로 수평, 수직 영역을 동시에 나눔<br>
  