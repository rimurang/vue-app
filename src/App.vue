<template>
  <div>
    <h1>{{ message }}</h1>
    <p>Vue 3 튜토리얼에 오신것을 환영합니다!</p>

    <h2>reactive 객체 실습</h2>

    <h3>이름을 입력해보세요</h3>
    <input type="text" v-model="name" placeholder="이름 입력" />님,
    <input type="text" v-model="age" placeholder="나이 입력" />살
    <p>안녕하세요, {{ name }}님! {{ name }}님의 나이는 {{ age }}살</p>

    <input type="text" v-model="user.firstName" placeholder="이름 입력" />
    <input type="text" v-model="user.lastName" placeholder="성 입력" />
    <p>안녕하세요, {{ user.lastName }}{{ user.firstName }}님! 랄랄라</p>

    <h3>카운터앱</h3>
    <p>현재 값 : {{ count }}</p>
    <button @click="countDecrease">-1</button>
    <button @click="countIncrease">+1</button>
    <button @click="countReset">초기화</button>

    <hr />

    <h2>컴포넌트 나누기 & 데이터 전달 (props, emit)</h2>

    <h3>나의 Todo 리스트</h3>
    <div class="form_wrap">
      <input v-model="newTodo" placeholder="할 일을 입력하세요" type="text" />
      <button @click="addTodo">추가</button>
    </div>

    <ul class="todo_list">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :item="todo"
        @remove="removeTodo(index)"
      >
      </TodoItem>

      <p v-if="todos.length === 0" class="empty">할 일이 없습니다.</p>
    </ul>

    <hr />

    <h2>조건부 렌더링과 반복 렌더링 완벽 이해</h2>

    <h3>조건부 렌더링</h3>
    <p v-if="score >= 90">A 학점</p>
    <p v-else-if="score >= 80">B 학점</p>
    <p v-else>C 학점</p>
    <p v-show="score >= 80">내 학점은 ? {{ score }}학점</p>
    <p v-show="visible">보이죠</p>
    <p v-show="invisible">안보이죠</p>

    <h3>반복 렌더링</h3>
    <ul>
      <li v-for="(fruit, index) in fruits" :key="index">
        {{ index + 1 }}. {{ fruit }}
      </li>
    </ul>

    <h3>렌더링 실습 : 점수에 따른 메시지와 과일 리스트 출력</h3>
    <div class="score-box">
      <input
        type="number"
        v-model="stScore"
        placeholder="점수를 입력하세요 (0~100)"
        min="0"
        max="0"
      />
    </div>
    <div class="grade-message">
      <p v-if="stScore >= 80" class="grade a">훌륭합니다</p>
      <p v-else-if="stScore >= 70" class="grade b">잘했어요</p>
      <p v-else-if="stScore >= 60" class="grade c">노력해봐요</p>
      <p v-else="stScore >= 50" class="grade d">다음엔 더 잘할 수 있어요</p>
    </div>

    <ul>
      <li v-for="(color, index) in colors" :key="index">
        {{ index + 1 }}. {{ color }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
import TodoItem from "./components/TodoItem.vue";

/* S: ref / reactive 실습 */
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
/* E: ref / reactive 실습 */

/* S: Todo 앱 */
const newTodo = ref("");
const todos = ref(["Vue 공부하기", "밥 먹기"]);

function addTodo() {
  // todo 추가
  if (newTodo.value.trim()) {
    // newTodo.value에 값이 있을때
    todos.value.push(newTodo.value); // todos에 추가
    newTodo.value = ""; // 초기화
  } else {
    alert("할 일을 입력해주세요.");
  }
}
function removeTodo(index) {
  // todo 삭제
  todos.value.splice(index, 1); //todos 배열에서 index 요소 제거
}
/* E: Todo 앱 */

/* S: 조건부 렌더링과 반복 렌더링 완벽 이해 */
const score = ref(85);
const visible = true;
const invisible = false;

const fruits = ["두리안", "망고", "푸릇"];

const stScore = ref(75);
const colors = ["초록", "빨강", "보라"];
/* E: 조건부 렌더링과 반복 렌더링 완벽 이해 */
</script>

<style scoped>
hr {
  margin: 30px 0;
}
input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 6px;
  margin: 0 2px;
}
button {
  padding: 8px 12px;
  border: none;
  background-color: #746dd6;
  color: white;
  border-radius: 6px;
  cursor: pointer;
  margin: 0 2px;
}

button:hover {
  background-color: #746dd6;
}
ul {
  display: flex;
  gap: 3px;
}
ul li {
  list-style: none;
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 6px;
  margin: 0 2px;
}
</style>
