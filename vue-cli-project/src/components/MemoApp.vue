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
            <memo-test v-for="memo in memos"
                    :key="memo.id"
                    :memoPropsFromMemoApp="memo" />
        </ul>
    </div>
</template>

<script>
import MemoForm from './MemoForm';
import MemoTest from './MemoTest';

export default {
    name: 'MemoApp',
    components: {
        MemoForm,
        MemoTest,
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