<template>
  <div class="mb-2 d-flex">
        <div>
            <input type="checkbox" :checked="todo.checked" @change="toggleCheckbox">
        </div>
        <span class="ml-3 flex-grow-1" :class="todo.checked ? 'text-muted' : '' " :style="todo.checked ? 'text-decoration: line-through':''">{{todo.text}}</span>
        <!--위 바인딩의 의미는 todo.checked가 체크되어 있다면 부트스트랩의 text-muted으로 변경하고 아니라면 아무것도 안함. 오른쪽도 동일(대신 글 가운데 줄이 들어감)  -->
        <button class="btn btn-danger btn-sm flex-grow-1" @click="clickDelete">Delete</button>
    </div>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object, //타입이 태그라 오브젝트로 프롭을 받아옴
            required: true //해당 타입이ㅣ아니라면 오류를 반환함.
        }
    },
    methods: {
        toggleCheckbox(e) {
            this.$emit('toggle-checkbox', { //emit를 통해 상위 부모 컴포넌트로 값을 보내줌
                id: this.todo.id,
                checked: e.target.checked
            })
        },
        clickDelete(){
            this.$emit('click-delete', this.todo.id); //emit를 통해 상위 부모 컴포넌트로 값을 보내줌
        }
    }
}
</script>

<style>

</style>