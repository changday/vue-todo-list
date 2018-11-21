<template>
  <div>
    <el-input
      v-model="inputValue"
      placeholder="输入以添加待办事项"
      clearable
      style="width: 300px"
      @keyup.enter.native="addTodoItem"
    >
    </el-input>
    <el-button style="margin-left: 10px" @click="addTodoItem">添加</el-button>
    <ul :class="{visibility: isVisibility}">
      <li
        v-for="(item, index) in todoItems"
        :key="index"
        :class="{finished: item.finished}"
        @mousedown="finishItem(item)"
        @mouseup="removeTodoItem(index)"
      >
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      inputValue: '',
      todoItems: [],
      isVisibility: true
    }
  },
  methods: {
    addTodoItem() {
      if (this.inputValue.trim()) {
        this.todoItems.push({ text: this.inputValue, finished: false });
        this.inputValue = '';
        this.isVisibility = false;
      }
    },
    removeTodoItem(index) {
      this.todoItems.splice(index, 1);
      if (!index) {
        this.isVisibility = true;
      }
    },
    finishItem(item) {
      item.finished = !item.finished
    }
  }
}
</script>

<style scoped>
  .finished {
    text-decoration: line-through;
  }
  ul.visibility {
    visibility: hidden;
  }
  ul {
    box-sizing: border-box;
    padding: 0;
    width: 300px;
    border: 1px solid #eee;
    border-radius: 4px;
    
  }
  ul li {
    list-style: none;
    padding: 12px 18px;
    border-bottom: 1px solid #eee;
  }
  ul li:last-child {
    border-bottom: none;
  }
  ul li:hover {
    background-color: #eee;
  }
  
</style>