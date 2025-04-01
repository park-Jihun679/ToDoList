<script setup>
const props = defineProps({
  todo: {
    type: Object,
  },
});
const emits = defineEmits(['finished-todo', 'remove-todo']);

const finishedTodo = (id) => {
  emits('finished-todo', id);
};

const removeTodo = (id) => {
  emits('remove-todo', id);
};
</script>

<template>
  <div class="items-header">
    <span class="title">오늘의 할일 리스트</span>
    <span class="time">입력/완료 시간</span>
  </div>
  <ul class="items">
    <li class="item">
      <span class="todo">{{ todo.text }}</span>
      <span class="input-time">{{ todo.createdAt }}</span>
      <span class="finish-time">{{ todo.finishedAt }}</span>
      <i class="fa-solid fa-check" @click.stop="finishedTodo(todo.id)"></i>
      <i class="fa-solid fa-trash" @click.stop="removeTodo(todo.id)"></i>
    </li>
  </ul>
</template>

<style scoped>
/* ul */
.items {
  padding: 1rem;
  height: 500px;
  overflow-y: auto;
  min-height: 100px;
}
.items-header {
  display: flex;
  justify-content: space-between;
  padding: 1rem;
  background-color: #f5f5f5;
  font-weight: bold;
  border-bottom: 2px solid gray;
  position: sticky;
  top: 0;
  z-index: 10;
}
.items-header .title {
  flex: 2;
}

.items-header .time {
  flex: 1;
  text-align: right;
  padding-right: 20px; /* 필요하면 조절 */
}
/* li */
.item {
  display: flex;
  /* justify-content: space-between; */
  gap: 1rem;
  padding: 0.5rem 1rem;
  border-bottom: 1px solid lightgray;
  cursor: pointer;
  transition: 0.3;
}
.item:hover {
  background-color: #eae9ee;
}
/* li 체크 클릭됬을 때 */
.item.item_done span {
  opacity: 0.1;
  text-decoration: line-through;
}
.item span {
  flex: 1;
  text-align: left;
}
.item span:first-child {
  flex: 2;
}

.item .input-time {
  flex: 0.8;
  text-align: right;
}

.item .input-time.item_done {
  display: none;
}
.finish-time {
  display: none;
}
.item .item_done .finish-time {
  flex: 0.8;
  text-align: right;
}

/*  아이콘 */
.fa-check,
.fa-trash {
  font-size: 16px;
  transition: 0.3s;
}
.fa-check:hover {
  color: dodgerblue;
}
.fa-trash:hover {
  color: red;
  transform: scale(1.1);
}
</style>
