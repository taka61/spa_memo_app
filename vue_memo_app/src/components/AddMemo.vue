<template>
  <div v-if="!isAdding">
    <a class ="btn btn-outline-primary btn-sm" @click="openForm">+</a>
  </div>

  <div v-else>
    <form v-on:submit.prevent>
      <textarea rows="5" cols="30" v-model="newMemo">タスクを入力</textarea>
      <button @click="addMemo">追加</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isAdding: false,
      newMemo: '',
    }
  },
  methods: {
    openForm() {
      this.isAdding = true
    },
    addMemo() {
      if (this.newMemo === '') return
      this.$emit('new-memo', this.newMemo);
      this.isAdding = false
      this.newMemo= '';
    }
  }
};
</script>

<style scoped>
textarea {
  background: #F9F9F9;
  width: 230px;
  height: 230px;
  padding: 9px;
  margin-top: 30px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font: 300 15px Roboto;
  display: flex;
  }

a {
    margin-left: 40px;
}

button {
  background: #2e99a9;
  color: #fff;
  padding: 5px 20px;
  margin-top: 20px;
  margin-left: 10px;
  border-radius: 5px;
  width: 200px;
  }
</style>
