> [NHN Meetup 블로그](https://meetup.toast.com/posts/160)에서 많은 양의 dom을 동적으로 렌더링 하기위해 성능을 최적화 하는 방법을 알게 되었습니다.  
> 그 중에서 브라우저 렌더링에 중요한 `Reflow`와 `Repaint` 개념에 대해 정리하고자 글을 남깁니다.


# 1. Reflow
"Reflow"는 모든 엘리먼트의 위치와 길이 등을 다시 계산하는 것입니다.  
따라서, 문서의 일부 혹은 전체를 다시 렌더링 합니다.  
참고로 단일 element를 변경해도, 하위 element 혹은 상위 element 등에 영향을 미칠 수 있습니다.

# 2. Repaint
`Repaint`는 `Reflow` 과정이 끝난 후 재 생성된 렌더 트리를 다시 그리게 되는 과정입니다.
`Repaint`는 `Reflow`의 하위 과정입니다. 하지만 `Reflow`가 발생하지 않고, `Repaint`만 발생하는 경우도 있습니다.
`Layout`에 영향을 주지 않고, element 개별의 변화일 때는 `Repaint`만 일어납니다.

# 3. Reflow가 일어나는 경우(일부분)
* DOM element 추가, 제거 또는 변경
* CSS 스타일 추가, 제거 또는 변경
* CSS `animation`과 `transition`
* `offsetWidth`와 `offsetHeight` 사용
* User interaction
  * 창 크기 조정, font size 혹은 종류 변경 등등...

# 4. 성능 저하 최소화 하기
* `javascript`를 통해 리스트를 추가하는 경우, DOM Fragment를 통해 추가합니다.
* 최대한 말단의 Node class 변경을 합니다.
* inline style을 사용하지 않습니다.
* animation이 들어간 element는 `position: fixed` 혹은 `position: absolute`로 지정합니다.
* Layout을 위한 `<table>`은 피합니다.
* `display: none;`으로 숨겨진 엘리먼트는 변경될 때, `Reflow`나 `Repaint`를 일으키지 않습니다.

# 참조
* [브라우저 동작 과정 - Naver D2](https://d2.naver.com/helloworld/59361)
* https://wonism.github.io/reflow-repaint/
* https://webclub.tistory.com/346
