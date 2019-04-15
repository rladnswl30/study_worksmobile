## SPA ?
- 단일 페이지 애플리케이션(Single Page Application)
- 기존 서버 사이드 렌더링과 비교할 때, 네이티브 앱과 유사한 사용자 경험 제공.

## SPA와 기존 웹 방식의 차이
- 기존 웹 방식
    - link tag를 사용하는 전통적인 웹 방식은 페이지 요청 시마다 정적 리소스가 다운로드
    - 전체 페이지를 재렌더링하는 방식을 사용하여 사용성이 떨어지고, 비효율적
- SPA
    - 모든 정적 리소스를 최초에 한번 다운로드
    - 새로운 페이지 요청 시 필요한 데이터만 전달받아 필요한 페이지만 갱신하여 트래픽 감소.
    - 전체 페이지를 재렌더링하는 대신 변경된 부분만 갱신하여 새로고침이 발생하지 않아 네이티브 앱과 유사한 사용자 경험 제공.

SPA 핵심은 사용자 경험(UX) 향상에 있으며, 애플리케이션 속도 향상과 Mobile First 전략에 부합.

## 대표적인 SPA Framework
- React (https://github.com/facebook/react)
- Vue (https://github.com/vuejs/vue)
- Angular (https://github.com/angular/angular)

## React VS Vue
### 비교
- React
    - facebook 등 큰 기업의 지원 및 수많은 library
    - 가장 거대한 community
    - Virtual dom
    - 템플릿 코드가 js안에 들어간 JSX문법
    - React native
    - redux
    - SSR(Server side rendering)으로 next.js를 통한 SEO 지원

- Vue
    - 가장 가파르게 성장하고 있으며, star 수 1등
    - 낮은 러닝커브
    - Virtual dom
    - .vue 안에 js, 마크업이 모두 들어가있다.
    - 양방향 바인딩 (view <-> data) (https://velopert.com/3136)
    - vuex
    - SSR로 nuxt.js를 통한 SEO 지원

### 데이터를 바꾸는 방식(Mutating the data)
- vue
```javascript
data() {
    return {
        name : 'woonji'
    }
}
```
데이터 객체를 생성하고 data를 자유롭게 업데이트 할 수 있다.
this.name = 'john'을 호출하여 값을 변경시킬 수 있다.  
- react
``` javascript
constructor(props) {
    super(props);
    this.state = {
        name : 'woonji'
    }
}
```
state 객체를 만들고 data를 변경실킬 때에는 setState를 해주어야 한다.  
this.state.name을 하여 참조하고, this.state.name = 'john'이 아닌, this.setState({name : 'john'})으로 값을 변경시킬 수 있다.  

```
※ vue는 data를 업데이트 할 때마다 setState를 알아서 결합해주는데, react는 왜 직접 setState로 변경시켜주어야 하는가?
react lifecycle 중, "componentWillReceiveProps, shouldComponentUpdate, componentWillUpdate, render, componentDidUpdate"를 state를 변경할 때마다 다시 실행되어야 한다.  
이를 위해 setState를 사용하여 값을 변경한다.
```

### 간단한 코드 비교
할일을 생성해보자~
- react
```javascript
createNewToDoItem = () => {
    this.setState( ({ list, todo }) => ({
    list: [
      …list,
      {todo}
    ],
    todo: ''
   })
  );
};

handleInput = e => {
    this.setState({
        todo: e.target.value
    });
};
```

```jsp
<input type=”text” value={this.state.todo} onChange={this.handleInput} />
<button className="ToDo-Add" onClick={this.createNewToDoItem}>+</button>
```

- vue
```javascript
createNewToDoItem() {
    this.list.push(
        {
            'todo': this.todo
        }
    );
    this.todo = '';
}
```

```jsp
<input type="text" v-model="todo" />
<div class="ToDo-Add" @click="createNewToDoItem()">+</div>
```

- react는 setState를 통해서 값을 변경하고, vue는 직접 값을 변경하였다.
- react는 onChange로 양방향 바인딩을 해주고, vue는 v-model을 통해 양방향 바인딩을 해준다.
그 외로
- react의 자식 컴포넌트는 this.props를 통해 부모 함수에 접근이 가능하고, vue는 부모 컴포넌트 내부에서 자식에게 event를 보낸다.
- 이벤트 리스너 전달 시 react는 onClick, vue는 @click

## 결론
개인적으로 문법은 vue가 훨씬 간결하고 가독성이 좋으며, 익숙한 것 같다.
vue처럼 template에 기반한 앱이 가독성이 좋은 반면, 복잡한 규모의 앱에서는 유지보수의 어려움이 있다고 한다.
반면 react는 application data의 불변 속성(state)이 처음에는 익숙하지 않아 어렵지만, 복잡한 규모의 앱에서는 더 좋다고 한다.


참고 )
https://medium.com/javascript-in-plain-english/i-created-the-exact-same-app-in-react-and-vue-here-are-the-differences-e9a1ae8077fd
https://github.com/sunil-sandhu/vue-todo/blob/master/src/ToDo.vue
https://github.com/sunil-sandhu/react-todo/blob/master/src/ToDo.js