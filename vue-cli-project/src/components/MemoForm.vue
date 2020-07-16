<template>
    <div class="memo-form">
        <!-- form 을 이용하여 사용자가 입력할 수 있는 fieldset를 추가한다. -->
        <!-- type이 submit으로 선언된 등록하기 버튼을 누르면 이벤트를 동기방식으로 실행시키기 떄문에 현재의 브라우저가 리로드된다.
            메모예제에서는 리로드를 하지않고 값을 등록해야하기 때문에 개발자가 event.preventDefault 함수를 사용하여 리로드를 막아야하지만
            Vue 에서는 prevent 옵션을 제공해준다.
            addMemo 라는 콜백 함수를 생성해줘서 addMemo에서 사용자가 입력한 제목과 내용에 대한 데이터를 부모 컴포넌트인 MemoApp 컴포넌트에 emit 을 이용하여 전파한다. -->
        <form @submit.prevent="addMemo">
            <fieldset>
                <div>
                    <!-- title 을 v-model 을 이용하여 연결한다. -->
                    <!-- v-model 을 이용하여 입력 필드에 연결하게되면 데이터 바인딩이 되어 사용자가 입력할때마다 변수값이 갱신된다. -->
                    <input class="memo-form__title-form"
                            type="text"
                            v-model="title"
                            placeholder="메모의 제목을 입력해주세요."/>
                    <textarea class="memo-form__content-form"
                                v-model="content"
                                placeholder="메모의 내용을 입력해주세요."/>
                    <!-- reset.css 에서 추가한 폰트어썸은 다음과 같이 클래스를 이용하여 아이콘을 사용할 수 있다. -->
                    <button type="reset"><i class="fas fa-sync-alt"></i></button>
                </div>
                <button type="submit"> 등록하기 </button>
            </fieldset>
        </form>
    </div>
</template>
<script>
export default {
    // 컴포넌트의 이름을 MemoForm으로 한다.
    name: 'MemoForm',
    data() {
        return {
            // 사용자가 입력할 제목과 콘텐츠가 저장될 데이터의 키와 값
            title: '',
            content: ''
        }
    },
    methods: {
        addMemo () {
            /*
            * 기존 메모의 ID 를 임의로 생성하여 메모 데이터를 만든 과정
            *
            // 비구조화 할당??? 구문을 이용하여 변수를 선언한다.????
            // 비구조화 할당 구문 : 객체의 속성을 해제하여 그 값을 각각의 변수에 담을 수 있도록하는 자바스크립트의 표현식 문법이다.
            const { title, content } = this;
            // 데이터의 고유한 식별자를 생성한다.
            const id = new Date().getTime();

            // 제목이나 내용을 입력하지 않은 경우 
            const isEmpty = title.length <= 0 || content.length <= 0;
            if (isEmpty) {
                alert("값을 입력해주세요.");
                return false;
            }

            // addMemo 이벤트를 발생시키고 payload로 사용자가 입력한 데이터를 넣어준다.
            this.$emit('addMemo', { id, title, content });

            // 부모 컴포넌트에 데이터를 전파한 후 입력창의 데이터를 다시 초기화한다
            this.resetField();
            */

            /*
            * RESTful API 를 통해 생성된 메모 ID 를 사용하여 메모 데이터를 만드는 과정
            *
           */
            console.log("MemoForm >> this :: ", this);
            const { title, content } = this;
            const isEmpty = title.length <= 0 || content.length <= 0;
            if (isEmpty) {
                alert("값을 입력해주세요.");
                return false;
            }
            this.$emit('addMemo', { title, content });
            this.resetField();
        },
        resetField () {
            this.title = '';
            this.content = '';
        }
    },
}
</script>
<!-- scoped 를 사용하여 해당 컴포넌트에서만 스타일이 적용될 수 있도록 할 수 있다. -->
<style scoped>
    .memo-form {
        margin-bottom: 24px;
        padding-bottom: 40px;
        border-bottom: 1px solid #eee;
    }
    .memo-form form fieldset div {
        position: relative;
        padding: 24px;
        margin-bottom: 20px;
        box-shadow: 0 4px 10px -4px rgba(0, 0, 0, 0.2);
        background-color: #ffffff;
    }
    .memo-form form fieldset div button[type="reset"] {
        position: absolute;
        right: 20px;
        bottom: 20px;
        font-size: 16px;
        background: none;
    }
    .memo-form form fieldset button[type="submit"] {
        float: right;
        width: 96px;
        padding: 12px 0;
        border-radius: 4px;
        background-color: #ff5a00;
        color: #fff;
        font-size: 16px;
    }
    .memo-form form fieldset .memo-form__title-form {
        width: 100%;
        margin-bottom: 12px;
        font-size: 18px;
        line-height: 26px;
    }
    .memo-form form fieldset .memo-form__content-form {
        width: 100%;
        height: 66px;
        font-size: 14px;
        line-height: 22px;
        vertical-align: top;
    }
    .memo-form input:focus {
        outline: none;
    }
</style>