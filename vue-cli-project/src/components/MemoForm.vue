<template>
    <div class="memo-form">
        <!-- form 을 이용하여 사용자가 입력할 수 있는 필드를 추가한다. -->
        <form>
            <fieldset>
                <div>
                    <input class="memo-form__title-form"
                            type="text"
                            placeholder="메모의 제목을 입력해주세요."/>
                    <textarea class="memo-form__content-form"
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
    name: 'MemoForm'
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