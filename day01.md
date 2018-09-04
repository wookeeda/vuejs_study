## 01.Intro
    유연함, 가벼움, 학습곡선 > angular, react

    MVVM 패턴 : view, view model, model

    개발 환경 : npm, vscode, vue-cli, vuejs devtool(chrome)


## 02.기본 디렉티브
    v-text: innerText 속성에 연결됨, 태그 문자열을 HTML 인코딩하여 나타내기 때문에 화면에는 태그 문자열이 그대로 나타남.
    v-html: HTML태그를 브라우저에서 파싱, XSS 취약, v-text 사용할 것.
    v-bind: 
        element의 content 영역이 아닌 속성을 바인딩. ex) input tag의 value
        줄여 쓸 수 있음. v-bind:src -> :src

    * 앞의 디렉티브들은 단방향, HTML 요소에서 값을 변경하여도 모델 객체의 값이 바뀌지는 않음.
    v-model: 양방향 데이터 바인딩

    v-if: 조건에 따라 렌더링을 여부 결정
    v-show: 렌더링 후 display 속성(none) 여부 결정
    * 화면이 자주 변경될 때는 v-show

    v-if, v-else-if, v-else
    v-for
        ex1) <tr v-for="(contact, index) in  contacts">
                <td>{{contact.no}}</td>
                <td>{{contact.name}}</td>
                <td>{{contact.age}}</td>


        ex2) <option v-for="(val, key, index) in object" v-bind:value="key">{{index+1}} : {{val}}</option>


    v-for, v-if 함께 사용 시, v-for 먼저 수행되고 v-if 적용
    ex) <tr v-for"(contact, index) in contacts" v-if="contact.age > 20" >


    template 태그 : 여러 element 그룹을 반복 렌더링 할 때,
    <template v-for="(contact, index) in contacts">
        <tr>
            <td>{{contact.no}}</td>
            <td>{{contact.name}}</td>
            <td>{{contact.age}}</td>
        </tr>
        <tr class="divider" v-if="index % 5 === 4">
            <td colspan="3"></td>
        </tr>
    </template>

### *배열 데이터 변경에 관한 문제
    list.contacts[0] = {"no": 1000, name="맹", age="1000"};
    로 변경해도 화면에는 변화 없음
    : Vue 인스턴스 내부의 감시자가 추적하지 않음
    -> Vue.set method 사용
    : Vue.set(list.contacts[0], {"no": 1000, name="맹", age="1000"});
    -> 자바스크립트 배열 객체가 지원하는 메서드를 사용하면 추적 가능
    : push, pop, shift, unshift, splice, filter, contact, slice, reduce 등
    