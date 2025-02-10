Controlled Component는 리액트 상태(stats)를 통해입력값을 제어하는 컴포넌트를 말한다.  
이 방식에서는 입력 요소의 값(value)을 리액트 상태와 동기화하고, 사용자가 입력을 변경할 때마다 onChange 이벤트 핸들러를 통해 상태를 업데이트한다.  
useState를 활용한 input value를 제어하는 상황을 예시로 들 수 있다.  
value는 리액트 상태로 관리되며, onChange 이벤트가 발생할 때마다 상태가 업데이트된다.  
Controlled Component의 주요 장점은 입력값이 리액트의 상태로 관리되므로, 입력값을 쉽게 검증하고, 변경할 수 있으며, 복잡한 폼 로직을 처리하는 데 유리하다는 것이다.  

Uncontrolled Component는 리액트의 상태가 아닌, DOM 자체가 입력값을 제어하는 방식이다.  
즉, 입력 요소의 값은 DOM에서 직접 관리되며, 리액트는 이를 제어하지 않는다.  
이 방식에서는 ref를 사용하여 DOM 요소에 직접 접근해 값을 읽어오거나 조작할 수 있다.  

input과 관련 된 ref는 useRef를 상요해 생성된 참조 객체로, 입력값을 직접 접근하고 조작할 수 있다.  
Uncontrolled Component는 상대적으로 간단한 폼이나 초기값이 중요한 상황에서 사용할 수 있다.  

### Controlled Component와 Uncontrolled Component를 통해 상태를 관리하는 것 중 어느 상황에서 어떤 방법을 선택해야 하나?

ref를 사용하면 DOM을 통해 직접 접근하여 값을 읽어오기 때문에, 단순한 입력 필드가 포함된 폼에서 ref를 사용하는 것이 더 간단하고 성능이 좋을 수 있다.  
사용자가 제출 버튼을 클릭했을 때만 입력 값을 가져오면 되는 경우를 예로 들 수 있다.  

만약에 값을 입력할 때마다 유효성 검정을 실시간으로 해주어야하는 경우에는 Controlled Component를 사용하는 것이 좋다.

----
- [[10분 테코톡] 세인의 제어 컴포넌트와 비제어 컴포넌트](https://www.youtube.com/watch?v=PBgQKK6nelo&t=253s)
