<template>
  <div>
    <h1>{{ message }}</h1>
    <p>Vue 3 튜토리얼에 오신것을 환영합니다!</p>

    <h2>reactive 객체 실습</h2>

    <h3>이름을 입력해보세요</h3>
    <input type="text" v-model="name" placeholder="이름 입력" />
    님,
    <input type="text" v-model="age" placeholder="나이 입력" />
    살
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
      ></TodoItem>

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

    <hr />

    <h2>동적 스타일과 클래스 바인딩</h2>

    <h3>좋아하는 빵 선택하기</h3>

    <div class="fruit-wrap">
      <ul class="fruit-list">
        <li
          v-for="(dessert, index) in desserts"
          :key="index"
          :class="{ selected: selectedDesserts === dessert }"
          @click="selectDesserts(dessert)"
        >
          {{ dessert }}
        </li>
      </ul>

      <p v-if="selectedDesserts" class="result">
        당신이 선택한 빵은
        <strong>{{ selectedDesserts }}</strong>
        입니다!
      </p>
      <p :style="{ color: isRed ? 'red' : 'blue' }">:style 테스트</p>
    </div>

    <hr />

    <h2 class="final">최종 실습 - 메모장앱 만들기</h2>
    <input v-model="newMemo" type="text" placeholder="메모를 입력하세요." />
    <button @click="addMemo">추가</button>

    <ul class="memo-list">
      <MemoItem
        v-for="(memo, index) in memos"
        :key="index"
        :text="memo"
        @delete="deleteMemo(index)"
      ></MemoItem>
    </ul>

    <p v-if="memos.length === 0" class="empty">메모가 없습니다.</p>

    <ul class="memo-step">
      <li>[사용자가 입력창에 새 메모 작성]</li>
      <li>↓ (v-model="newMemo")</li>
      <li>[추가 버튼 클릭 → addMemo()]</li>
      <li>↓</li>
      <li>[memos 배열에 새 항목 추가]</li>
      <li>↓</li>
      <li>[v-for로 각 메모 출력 → MemoItem 컴포넌트로 전달]</li>
      <li>↓</li>
      <li>[삭제 버튼 클릭 → emit('delete') → 부모에서 deleteMemo(index)]</li>
      <li>↓</li>
      <li>[memos 배열에서 항목 제거]</li>
      <li>↓</li>
      <li>[watch로 localStorage에 자동 저장]</li>
    </ul>

    <hr />

    <h2 class="final" style="background: red">템플릿 문법 요약</h2>
    <table>
      <thead>
        <tr>
          <th>문법</th>
          <th>역할</th>
          <th>예시</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>
            <pre v-pre>
<code>{{ exname }}</code></pre>
          </th>
          <td>출력</td>
          <td>
            <pre v-pre>
<code>&lt;p&gt;{{ exname }}&lt;/p&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>v-model</th>
          <td>양방향 바인딩</td>
          <td>
            <pre v-pre>
<code>&lt;input v-model="exmsg" /&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>v-if / v-else</th>
          <td>조건부 렌더링</td>
          <td>
            <pre v-pre>
<code>&lt;p v-if="count > 0">Positive&lt;/p&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>v-for</th>
          <td>리스트 렌더링</td>
          <td>
            <pre v-pre>
<code>&lt;li v-for="item in items"&gt;{{ item }}&lt;/li&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>:key</th>
          <td>리스트 식별</td>
          <td>
            <pre v-pre><code>&lt;li :key="index"&gt;&lt;/li&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>:class</th>
          <td>조건부 클래스 적용</td>
          <td>
            <pre
              v-pre
            ><code>&lt;div :class="{ active: isActive }"&gt;&lt;/div&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>:style</th>
          <td>인라인 스타일 바인딩</td>
          <td>
            <pre
              v-pre
            ><code>&lt;p :style="{ color: 'red' }">&gt;">제출&lt;/button&gt;</code></pre>
          </td>
        </tr>
        <tr>
          <th>props / emit</th>
          <td>부모-자식 통신</td>
          <td>자식은 props 받고 emit으로 이벤트 발생</td>
        </tr>
      </tbody>
    </table>

    <h2 class="final" style="background: red">
      Composition API 주요 기능 요약
    </h2>
    <table>
      <thead>
        <tr>
          <th>함수</th>
          <th>역할</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>ref()</td>
          <td>단일 값 반응형 상태</td>
        </tr>
        <tr>
          <td>reactive()</td>
          <td>객체/배열 반응형 상태</td>
        </tr>
        <tr>
          <td>watch()</td>
          <td>상태 변화 감지</td>
        </tr>
        <tr>
          <td>onMounted()</td>
          <td>컴포넌트 마운트 시 실행</td>
        </tr>
        <tr>
          <td>defineProps()</td>
          <td>자식 컴포넌트에서 props 받기</td>
        </tr>
        <tr>
          <td>$emit()</td>
          <td>자식 > 부모 이벤트 전송</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, watch } from "vue";
import TodoItem from "./components/TodoItem.vue";
import MemoItem from "./components/MemoItem.vue";

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

/* S: 동적 스타일과 클래스 바인딩 */
const desserts = ref(["휘낭시에", "밤식빵", "크림빵"]);
const selectedDesserts = ref("");
function selectDesserts(dessert) {
  selectedDesserts.value = dessert;
}

const isRed = true;
/* E: 동적 스타일과 클래스 바인딩 */

/* S: 메모장앱만들기 */
const newMemo = ref("");
const memos = ref([]);

function addMemo() {
  if (newMemo.value.trim()) {
    memos.value.push(newMemo.value.trim());
    newMemo.value = "";
    // 입력된 값을 newMemo에 바인딩
    // memos 배열에 메모 추가 + 입력값 초기화
  }
}
function deleteMemo(index) {
  // memo 삭제
  memos.value.splice(index, 1); //memos 배열에서 index 요소 1개 제거
}

//onMounted : 컴포넌트가 처음 로드될때 localStorage에서 저장된 메모들을 불러옴
onMounted(() => {
  const saved = localStorage.getItem("memos");
  if (saved) {
    memos.value = JSON.parse(saved);
  }
});
//watch : memos 값이 바뀔때마다  localStorage에 새로 저장
// deep:true : 배열 내부 항목 변경까지 감지 가능
watch(
  memos,
  (newVal) => {
    localStorage.setItem("memos", JSON.stringify(newVal));
  },
  { deep: true }
);
/* E: 메모장앱만들기 */
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

.fruit-list {
}
.fruit-list .selected {
  color: #fff;
  background: #000;
}

h2.final {
  color: #fff;
  background: #000;
}

.memo-list {
  display: flex;
  flex-direction: column;
}
.memo-step {
  display: flex;
  flex-direction: column;
  background: #202235;
  color: #6677b5;
  padding: 10px;
  text-align: left;
}
.memo-step li {
  border: 0;
  padding: 2px;
}
.memo-step li::marker {
  display: none;
}

table {
  width: 100%;
}
table th,
table td {
  border: 1px solid #ddd;
}
table thead th {
  background: #ddd;
}
table tbody th {
}
table tbody td {
}
</style>
