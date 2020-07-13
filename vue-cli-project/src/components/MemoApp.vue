<template>
    <div class="memo-app">
        <memo-form />
    </div>
</template>

<script>
import MemoForm from './MemoForm.vue';

export default {
    name: 'MemoApp',
    data() {
        return {
            memos: [],
        };
    },
    // created훅
    created() {
        // 만약 기존에 추가된 loaclstorage 에 데이터가 있다면 created 훅에서 localstorage의 데이터를 컴포넌트 내의 memos 데이터에 넣어주고 , 그렇지 않다면 그대로 빈 배별로 초기화한다.
        // 뭔말이냐?? 
        this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
    }
}
</script>