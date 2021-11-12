<template>
  <div>
    <form v-on:submit.prevent>
      <textarea rows="10" cols="40" v-model="selectedMemo"></textarea>
        <button class="is-edit" @click="updateMemo">編集</button>
        <button class="is-delete" @click="deleteMemo">削除</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ["newMemo"],
  data() {
    return {
      memos: [],
      selectedMemo: this.newMemo
    }
  },
  methods: {
    deleteMemo(index) {
      this.$emit('delete-memo',index);
    },
    updateMemo() {
      this.$emit('update-memo', this.selectedMemo);
    }
  }
};
</script>

<style scoped>
textarea {
  background: #F9F9F9;
  width: 350px;
  height: 400px;
  padding: 9px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font: 300 15px Roboto;
  display: flex;
  }

button {
  background: #2e99a9;
  color: #fff;
  padding: 5px 20px;
  margin-right: 20px;
  margin-top: 20px;
  border-radius: 5px;
  }

.is-edit {
  width: 240px;
}
</style>
