# ✨ 재밌는 기능 알아보기 ✨

## 랜덤 배열 만들기

```jsx
let num = [1, 2, 3, 4, 5];

num.sort(() => Math.random() - 0.5);
```

-   양수와 음수를 무작위로 반환하는 판별식을 이용해서 배열의 정렬 기능에 대입해 배열의 요소를 무작위로 바꾼다.
-   `Array.sort()`
    -   배열의 요소 순서를 변경한다.
    -   두 수의 크기를 비교할 때 리턴값 -1, 0, 1에 따라 두 값을 바꿀지 말지 결정한다.
    -   ASCII 우선순위에 따라 결정하기 때문에 숫자는 제대로 정렬이 안된다.
-   `Math.random()`

        -   0 ~ 1 미만의 값을 리턴 → 양수값만 출력 → 랜덤값이 한 방향으로만 편향 → 그것을 막기 위해서 0.5를 뺌
        -   반환받은 랜덤한 값에서 0.5를 빼면 음수 값과 양수 값을 무작위로 반환한다.
        -   `Array.sort()` 에 필요한 리턴값은 -1 과 1만 필요하다. (즉, 음수나 양수 중 하나만 리턴하면 됨)

              <img width="174" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-12-08_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4 19 01" src="https://user-images.githubusercontent.com/72817156/206423537-ecf2af7e-faec-4c8d-9e4e-7a6fea034f17.png">
              <br><br>

              <img width="190" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-12-08_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4 26 07" src="https://user-images.githubusercontent.com/72817156/206423493-6b52f75c-7e71-490d-92b0-219947840479.png">

    <br>

-   단점 : `Array.sort()` 함수는 위와 같은 용도로 만들어진 메서드가 아니기 때문에 순열의 빈도수가 균일하게 나오지 않는다.
    <br><br>

<aside>

### 💡 피셔-예이츠 셔플(Fishcer-Yates shuffle) 알고리즘 활용

-   배열 끝 요소부터 시작해 앞으로 하나씩 나아가면서 해당 요소 앞에 있는 임의의 요소와 해당 요소를 바꿔치기하는 알고리즘
-   위의 함수보다 더욱 고른 결과값을 획득할 수 있을 뿐만 아니라 피셔-예이츠 알고리즘은 ‘정렬' 연산도 없기 때문에 성능상 이점 또한 가지고 있음

    ```jsx
    function shuffle(array) {
        array.sort(() => Math.random() - 0.5);
    }

    // 1, 2, 3으로 만들 수 있는 모든 순열의 빈도를 세줍니다.
    let count = {
        123: 0,
        132: 0,
        213: 0,
        231: 0,
        321: 0,
        312: 0,
    };

    for (let i = 0; i < 1000000; i++) {
        let array = [1, 2, 3];
        shuffle(array);
        count[array.join("")]++;
    }

    // 만들 수 있는 모든 순열의 생성 빈도를 세서 출력해줍니다.
    for (let key in count) {
        alert(`${key}: ${count[key]}`);
    }
    ```

</aside>

<br><br>
Reference :

-   [Array.prototype.sort() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

-   [배열 요소 무작위로 섞기](https://ko.javascript.info/task/shuffle)
    <br><br>

## **insertAdjacentHTML 과 innerHTML 차이**

```jsx
$cardList.innerHTML += template;
// vs
$cardList.insertAdjacentHTML("beforeend", template);
```

-   `innerHTML`
    -   요소(element) 내에 포함된 HTML 또는 XML 마크업을 가져오거나 설정
    -   새로운 node로 교체하고, 추가적으로 파싱작업을 한다.
    -   가급적 사용을 피하는게 좋다.
        -   HTML 문자열을 그대로 추가하는 것이기 때문에 보안상으로도 문제가 되고 파싱 작업으로 인해 성능도 떨어진다.
-   `insertAdjacentHTML`
    -   HTML or XML 같은 특정 텍스트를 파싱하고, 특정 위치에 DOM tree 안에 원하는 node들을 추가한다.
    -   이미 사용중인 element 는 다시 파싱하지 않는다.
    -   element 안에 존재하는 element를 건드리지 않는다.
    -   추가 파싱없이 기존의 DOM tree안에 node를 추가하므로 innerHTML보다 작업이 덜 들고 빠르다.

<br><br>
Reference :

-   [Element.innerHTML - Web API | MDN](https://developer.mozilla.org/ko/docs/Web/API/Element/innerHTML)

-   [Element.insertAdjacentHTML() - Web API | MDN](https://developer.mozilla.org/ko/docs/Web/API/Element/insertAdjacentHTML)
    <br><br>

## CSS 속성 살펴보기

### transform-style: preserve-3d 은 무엇일까?

-   `transform-style` CSS 속성은 요소의 자식이 3D 공간에 배치되는지 또는 요소의 평면에서 병합되는지 여부를 설정한다.
-   `preserve-3d` 3D 효과가 적용된 요소의 자식 요소에 3D 효과가 전달
-   이 속성이 없다면 자식 요소에게 3D효과를 줄 수 없다.
-   IE 지원 X

<br><br>
Reference :

-   [transform-style: preserve-3d - 인프런 | 질문 & 답변](https://www.inflearn.com/questions/27627/transform-style-preserve-3d)
    <br><br>

### backface-visibility: hidden 은 무엇일까?

-   ‘뒷면을 보여준다’ 라는 의미
-   사용자의 시점에서 요소의 뒷면이 보이는지 여부를 설정하는 속성
    -   요소의 뒷면은 표시되는 앞면의 좌우반전된 이미지
    -   2D에서는 보이지 않지만 변형으로 인해 3D 공간에서 요소가 회전하면 뒷면이 보일 수 있다.
    -   이 속성은 원근감이 없는 2D 변환에는 영향을 주지 않는다.

<br><br>
Reference :

-   [backface-visibility - CSS&colon; Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/backface-visibility)

-   [CSS backface-visibility property](https://www.w3schools.com/cssref/css3_pr_backface-visibility.php)
