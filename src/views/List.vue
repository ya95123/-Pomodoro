<template>
  <div id="list">
    <b-form-input v-model="newtodo" @keydown.enter="addTodo"></b-form-input>
    <b-btn variant="success" @click="addTodo">新增</b-btn>
    <b-table-simple>
      <b-thead>
        <b-tr>
          <b-th>事項</b-th>
          <b-th>動作</b-th>
        </b-tr>
      </b-thead>
      <!-- 移動特效 -->
      <draggable v-model="todos" tag="tbody" v-bind="dragOption">
        <!-- 沒資料時 -->
        <b-tr v-if="todos.length == 0">
          <b-td colspan="2">沒有資料</b-td>
        </b-tr>
        <!-- 有資料時 -->
        <b-tr v-else v-for="(todo,index) in todos" :key="index">
          <b-td>
            <!-- 編輯狀態下 -->
            <b-form-input v-model="todo.model" v-if="todo.edit"></b-form-input>
            <!-- 取消編輯 -->
            <b-btn variant="link" class="text-danger" v-if="todo.edit" @click="cancelTodo(index)">
              <font-awesome-icon :icon="['fas', 'undo']"></font-awesome-icon>
            </b-btn>
            <!-- 儲存文字 -->
            <b-btn variant="link" class="text-success" v-if="todo.edit" @click="saveTodo(index)">
              <font-awesome-icon :icon="['fas', 'save']"></font-awesome-icon>
            </b-btn>
            <!-- Todo 裡的文字內容 -->
          <span v-else>{{ todo.name }}</span>
          </b-td>
          <!-- 動作 icon -->
          <b-td>
            <!-- 編輯icon -->
            <b-btn variant="link" class="text-primary" @click="editTodo(index)">
              <font-awesome-icon :icon="['fas', 'pen']"></font-awesome-icon>
            </b-btn>
            <!-- 刪除icon -->
            <b-btn variant="link" class="text-danger" @click="delTodo(index)">
              <font-awesome-icon :icon="['fas', 'times']"></font-awesome-icon>
            </b-btn>
          </b-td>
        </b-tr>
      </draggable>
    </b-table-simple>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // v-model 綁定這裡
      newtodo: '',
      dragOption: {
        animation: 200
      }
    }
  },
  methods: {
    addTodo () {
      this.$store.commit('addTodo', this.newtodo)
      console.log('add了')
    },
    delTodo (index) {
      this.$store.commit('delTodo', index)
    },
    editTodo (index) {
      this.$store.commit('editTodo', index)
    },
    cancelTodo (index) {
      this.$store.commit('cancelTodo', index)
    },
    saveTodo (index) {
      this.$store.commit('saveTodo', index)
    }
  },
  computed: {
    // 原本這只能寫入，但改成這楊還可以讀取↓ get 讀取 sey 寫入
    todos: {
      get () {
        return this.$store.getters.todos
      },
      set (value) {
        this.$store.commit('dragTodo', value)
      }
    }
  }
}
</script>
