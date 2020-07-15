<template>
    <li class="memo-item">
        <!-- 등록된 props 의 값을 각 DOM에 위치시킨다 -->
        <strong>{{ memoPropsFromMemoApp.title }}</strong>
        <p>{{ memoPropsFromMemoApp.content }}</p>
        <button type="button" @click="deleteMemo"><i class="fas fa-times"></i></button>
    </li>
</template>
<script>
export default {
    name: 'Memo',
    // 부모에게 내려받은 props 를 등록한다
    props: {
        memoPropsFromMemoApp: {
            type: Object
        }
    },
    methods: {
        deleteMemo () {
            const id = this.memoPropsFromMemoApp.id;
            // Memo 컴포넌트에서는 직접적으로 삭제를 하지않고, 부모 컴포넌트에서 삭제할 수 있게 인자로 id 값을 전달해준다. 전달된 id값은 deleteMemo라는 함수에서 수행한다.
            this.$emit('deleteMemo', id);
        }
    },  
}
</script>
<style scoped>
    .memo-item {
        overflow: hidden;
        position: relative;
        margin-bottom: 20px;
        padding: 24px;
        box-shadow: 0 4px 10px -4px rgba(0, 0, 0, 0.2);
        background-color: #fff;
        list-style: none;
    }
    .memo-item button {
        background: none;
        position: absolute;
        right: 20px;
        top: 20px;
        font-size: 20px;
        color: #e5e5e5;
        border: 0;
    }
    .memo-item strong {
        display: block;
        margin-bottom: 12px;
        font-size: 18px;
        font-weight: normal;
        word-break: break-all;
    }
    .memo-item p {
        margin: 0;
        font-size: 14px;
        line-height: 22px;
        color: #666;
    }
</style>