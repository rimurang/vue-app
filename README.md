# Vue 3 + Vite


## 1. 반응형 데이터 다뤄보기 (ref vs reactive)
- ref와 reactive의 차이를 이해하고 사용해본다
- 텍스트 입력으로 데이터를 바꾸는 실습을 해본다

ref : 문자열, 숫자 같은 단일 값 (.value 필요)
reactive : 객체, 배열 같은 복합 자료형 (바로 접근 가능)


## 2. 이벤트 처리 & 메서드로 데이터 바꾸기
- Vue에서 @click 등의 이벤트 처리 방법을 배운다
- 함수(메서드)를 작성해서 데이터를 바꾸는 방법을 익힌다
- 버튼을 눌러 숫자를 증가/감소하는 카운터 앱을 만들어본다

@click : 클릭 이벤트
@submit : 폼 제출 이벤트
@input : 입력창 변경 감지

@click="increase" = v-on:click="increase"


## 3. 컴포넌트 나누기 & 데이터 전달 (props / emit)
- Vue 컴포넌트를 파일로 나누어 재사용한다 (가독성, 유지보수 용이)
- 부모 > 자식 : props
- 자식 > 부모 : emit
- 간단한 todo 리스트 실습을 해본다


## 4. 조건부 렌더링 / 반복 렌더링
- v-if, v-else-if, v-else : 조건에 따라 필요한 요소만 DOM에 추가 (무거운 UI에 적합)
- v-show : DOM에 남아있고 스타일 display(none)로 노출 처리 (자주 토글되는 UI에 적합)
- v-for : 배열 순회, key 설정해야 성능&안정성 확보 
