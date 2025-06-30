<template>
  <div>
    <h1>{{ message }}</h1>
    <p>Vue 3 튜토리얼에 오신것을 환영합니다!</p>

    <h2>이름을 입력해보세요</h2>
    <input type="text" v-model="name" placeholder="이름 입력" />
    <p>안녕하세요, {{ name }}님!</p>
    <input type="text" v-model="age" placeholder="나이 입력" />
    <p>안녕하세요, {{ age }}님!</p>

    <h2>reactive 객체 실습</h2>
    <input type="text" v-model="user.firstName" placeholder="이름 입력" />
    <input type="text" v-model="user.lastName" placeholder="성 입력" />
    <p>안녕하세요, {{ user.lastName }}{{ user.firstName }}님! 랄랄라</p>

    <h2>카운터앱</h2>
    <p>현재 값 : {{ count }}</p>
    <button @click="countDecrease">-1</button>
    <button @click="countIncrease">+1</button>
    <button @click="countReset">초기화</button>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

/* ref / reactive 실습 */
const message = ref("🤖"); // 단일값
const name = ref("외계인"); // 단일값
const age = ref(5); // 단일값
age.value++;

const user = reactive({
  firstName: "라니",
  lastName: "고",
}); // 객체

/* 카운터 앱 */
const initCount = 0; // 초기값
const count = ref(initCount);

function countDecrease() {
  count.value--;
}
function countIncrease() {
  count.value++;
}
function countReset() {
  count.value = initCount; // 0으로 설정
}
</script>

<style scoped>
input {
  margin: 4px;
  padding: 4px;
}
</style>
