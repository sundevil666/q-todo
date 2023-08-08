<template>
  <q-page class="todo-list-page">
    <h1>Todo</h1>
    <q-input v-model="text" label="Add todo" class="q-mb-lg" @keyup.enter="addTodo">
      <template v-slot:append>
        <q-btn round dense flat icon="add" @click="addTodo" />
      </template>
    </q-input>
    <q-list separator bordered>

      <q-item
        v-for="(item, i) in todoList"
        :key="item.name"
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox  v-model="item.value" color="teal" />
        </q-item-section>
        <q-item-section
          :class="{'done': item.value}"
          @click="item.value = !item.value"
        >
          <q-item-label>{{ item.label }}</q-item-label>
        </q-item-section>
        <div
          v-if="item.value"
          class="cursor-pointer"
          @click="deleteTodo(i)"
        >
          &times;
        </div>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      todoList: [
        { label: 'td1', value: false },
        { label: 'td2', value: true },
        { label: 'td3', value: false },
      ],
      text: '',
    }
  },
  methods: {
    deleteTodo(i) {
      this.$q.dialog({
        title: 'Delete Todo',
        message: 'Are you sure you want to delete',
        cancel: true,
        persistent: true,
      }).onOk(() => {
        this.$q.notify({
          position: 'top',
          message: `Тудушка удалена ${this.todoList[i].label}`,git
        })
        this.todoList.splice(i, 1);
      })
    },
    addTodo() {
      if (this.text.length > 0) {
        this.todoList.push({ label: this.text, value: false })
        this.text = '';
      }
    },
  }
}

</script>
<style>
.done {
  text-decoration: line-through;
}
</style>
