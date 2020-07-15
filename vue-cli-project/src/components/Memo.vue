<template>
    <li class="memo-item">
        <!-- 등록된 props 의 값을 각 DOM에 위치시킨다 -->
        <strong>{{ memoPropsFromMemoApp.title }}</strong>
        <!-- dblclick : 더블클릭 이벤트 -->
        <p @dblclick="handleDdlClick">
            <template v-if="!isEditing">{{ memoPropsFromMemoApp.content }}</template>
            <!-- keydown.enter : 입력 후 엔터를 쳤을떄의 이벤트 -->
            <input v-else type="text" 
                            ref="content"
                            :value="memoPropsFromMemoApp.content" 
                            @keydown.enter="updateMemo"
                            />
        </p>
        <button type="button" @click="deleteMemo"><i class="fas fa-times"></i></button>
    </li>
</template>
<script>
export default {
    name: 'Memo',
    data() {
        return {
            isEditing: false
        }
    },
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
        },
        handleDdlClick () {
            console.log("handleDdlClick => ", this.$refs.content);
            this.isEditing = true;
            // input 에 등록해준 속성 중 ref 를 이용해 DOM에 접근할 수 있고 ref 를 뷰 인스턴스에 이 엘리먼트에 대한 정보를 줄 수 있다. id나 class 에 의존하지 않아도 되므로 좀 더 안전하다.
            // 하지만!!! vue 는 개발자가 DOM 을 다루지않게 하기 위한 것이므로 되도록 사용을 피하는게 좋다.
            // this.$refs.content.focus();
            // 위와 같이 this.$refs.content.focus(); 이렇게만 했을경우에는 $refs.content 가 감지되지 않아 콘솔에서 undefined 에러가 발생한다.
            // 이는 isEditing 값의 변경으로 인한 vue의 재랜더링이 아직 진행중이라 $refs.content라는 값이 없다는 것을 의미한다.
            // DOM의 업데이트를 하기 직전인 beforeUpdate 에서도 마찬가지로 감지되지 않는다.
            // DOM이 재랜더링 된 이후인 updated 에서는 데이터의 변화에 따라 감지될 수도 안될 수도 있다. ***즉, 데이터 변경에 따른 컴포넌트 재렌더링 순서가 보장되지않음을 알 수 있다!!!!!! 
            // 따라서 nextTick 함수를 사용하여 vue 의 데이터 갱신 후 UI까지 완료된 뒤에 nextTick에 있는 콜백 함수를 최종적으로 수행하게 됨으로써 우회할 수 있다!
            this.$nextTick(() => {
                this.$refs.content.focus();
            })
            // 위 구문은 아래와 같이 풀어서 사용도 가능하다.
            // this.$nextTick(function () {
            //     this.$refs.content.focus();
            // })
        },
        updateMemo (e) {
            console.log("updateMemo => ", e);
            const id = this.memoPropsFromMemoApp.id;
            var content = e.target.value.trim();
            console.log("updateMemo => ", content);
            if (content.length <= 0) {
                //alert("내용이 비어있습니다. 입력해주세요.");
                content = this.memoPropsFromMemoApp.content;
            }
            this.$emit('updateMemo', { id, content });
            this.isEditing = false;
        }
    },  
    beforeUpdate() {
        console.log("beforeUpdate => ", this.$refs.content);
    },
    updated() {
        console.log("updated => ", this.$refs.content);
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
    .memo-item p input[type="text"] {
        box-sizing: border-box;
        width: 100%;
        font-size: inherit;
        border: 1px solid #999;
    }
</style>