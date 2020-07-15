<template>
    <div class="memo-app">
        <!-- v-on 을 이용하여 자식 컴포넌트인 MemoForm 컴포넌트의 addMemo 이벤트 콜백함수로 연결한다 -->
        <!-- <memo-form v-on:addMemo="addMemo" /> 아래 코드와 같은 의미이다 -->
        <memo-form @addMemo="addMemo" />
        <ul class="memo-list">
            <!-- memos 배열에 있는 값을 v-for 를 사용하여 데이터를 가져와 랜더링해준다 -->
            <!-- 사용자 지정 태그를 작성할때!!  케밥 케이스로 작성하는것이 보편적 -->
            <!-- 사용자 지정 태그를 작성할떄 컴포넌트 명이 Test 라면 <test /> 가 되고, TestCompo 라면 <test-compo /> 가 된다!! 책 대충 읽었다가 혼자 의문에 빠져서 뻘짓함 ㅡㅡㅋ  -->
            <!-- v-for 사용시 2.2.0 이상에서는 key 값을 필수로 등록을 해줘야한다. -->
            <!-- 삭제 기능을 구현하기 위해 자식 컴포넌트에서 정한 deleteMemo 함수명을 리스너로 등록해준다. -->
            <!-- 수정 기능을 구현하기 위해 자식 컴포넌트에서 정한 updateMemo 함수명을 리스너로 등록해준다. -->
            <memo v-for="memo in memos"
                    :key="memo.id"
                    :memoPropsFromMemoApp="memo" 
                    @deleteMemo="deleteMemo"
                    @updateMemo="updateMemo"
                    />
        </ul>
    </div>
</template>

<script>
import MemoForm from './MemoForm';
import Memo from './Memo';

export default {
    name: 'MemoApp',
    components: {
        MemoForm,
        Memo,
    },
    data() {
        return {
            memos: [],
        };
    },
    // created훅
    created() {
        // 만약 기존에 추가된 loaclstorage 에 데이터가 있다면 created 훅에서 localstorage의 데이터를 컴포넌트 내의 memos 데이터에 넣어주고 , 그렇지 않다면 그대로 빈 배열로 초기화한다.
        this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
    }, 
    methods: {
        addMemo (payload) {
            // MemoForm 에서 올려 받은 데이터를 먼저 컴포넌트 내부 데이터에 추가한다
            this.memos.push(payload);
            // 내부 데이터를 문자열로 변환 후 로컬 스토리지에 저장한다
            this.storeMemo();
            // 로컬스토리지에 저상됨을 확인하려면 개발자 도구의 Application 탭에서 Storage->LocalStorage에서 현재 ip와 port가 적힌 곳에서 확인이 가능하다
        },
        storeMemo () {
            const memosToString = JSON.stringify(this.memos);
            localStorage.setItem('memos', memosToString);
        },
        deleteMemo (id) {
            //console.log("id ::: " + id);
            //console.log("this.memos ::: " + JSON.stringify(this.memos));

            // 자식 컴포넌트에서 인자로 전달해주는 id에 해당하는 메모 데이터의 인텍스를 찾는다.
            /*
            const targetIndex = this.memos.findIndex(function(data){
                return data.id === id;
            })
            */
            // 위의 코드는 return이 간단한 한줄짜리일 경우 람다식을 통해 아래와 같이 줄일 수 있다
            //const targetIndex = this.memos.findIndex(data => data.id === id);
            // 또는
            // 아래와 같이 길게 늘여쓸 수도 있다.
            /* 
            const targetIndex = this.memos.findIndex(function(data, index) {
                if (index === 0) {
                    return false;
                }else{
                    return data.id === id;
                }
            })
            */
            // 위 코드로 공부를 해보자면 findIndex 는 콜백 함수가 있어야하는 함수이다.
            // 따라서 함수를 변수에 담아 따로 정의를 할 수도 있다.
            /*
            const testFunc = function(data, index, array) {
                //(local function)(data: any, index: any, array: any): void
                // 로컬 함수라고 말한다. 로컬함수는 위와 같이 세가지 인자값을 가지고 있고, boolean 값을 return한다.
                console.log(data + ", " + index + ", " + array);
                return data.id === id;
            }
            const targetIndex = this.memos.findIndex(testFunc);
            */
            const targetIndex = this.memos.findIndex(data => data.id === id);
            //console.log("targetIndex >>> "+targetIndex);
            // 삭제 - splice 함수를 사용 : this.memos 배열에 있는 값들 중에 targetIndex를 포함한 한개 요소 제거 = 즉, targetIndex가 3이라면 3에 해당하는 값만 배열에서 제거한다.
            this.memos.splice(targetIndex, 1);
            // 삭제한 후 데이터를 로컬 스토리지에 다시 저장한다.
            this.storeMemo();
        },
        updateMemo (payload) {
            const { id, content } = payload;
            const targetIndex = this.memos.findIndex(v => v.id === id);
            const targetMemo = this.memos[targetIndex];
            // ...변수 : javacript 문법으로써 ES6에 추가된 spread 연산자라고 한다. ES6을 넘어 ES9에는 객체 또한 spread 연산자 사용이 가능합니다.
            /*
            const obj1 = {a: 1, b: 2}
            const obj2 = {c: 3}
            console.log({...obj1, ...obj2}) // {a: 1, b: 2, c: 3}
            // 객체 합치기에 사용할 수 있습니다.

            const copiedObj = {...obj1}
            console.log(copiedObj) // {a: 1, b: 2}
            // 객체 복사에 사용할 수 있습니다.

            const obj3 = {...obj1, b: 'b'}
            console.log(obj3) // {a: 1, b: 'b'}
            // 기존 객체의 값을 수정해서 새로운 객체 만들기에 사용할 수 있습니다.
            */
            // 수정 - splice 함수를 사용 : this.memos 배열에 있는 값들 중에 targetIndex를 포함한 한개 요소 제거하고 그 자리에 세번쨰 인자의 값 또는 객체를 넣어준다. = 즉, targetIndex가 3이라면 3에 해당하는 값만 배열에서 제거하고, 3에 세번째 인자 값을 넣어준다.
            this.memos.splice(targetIndex, 1, { ...targetMemo, content });
            this.storeMemo();
        }

    },
}
</script>

<style scoped>
    .memo-list {
        padding: 20px 0;
        margin: 0;
    }
</style>