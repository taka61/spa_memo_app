<template>
  <div id="app">
    <div class="container">
      <h1>Memo List</h1>
      <div class="left-side">
        <index-memo :memos="memos" @edit-memo="editMemo"></index-memo>
        <add-memo @new-memo="addMemo"></add-memo>
      </div>

      <div class="right-side" v-if="isEditing">
        <change-memo :newMemo="newMemo" @delete-memo="deleteMemo" @update-memo="updateMemo"></change-memo>
      </div>
    </div>
  </div>
</template>

<script>
import IndexMemo from './IndexMemo.vue';
import AddMemo from './AddMemo.vue';
import ChangeMemo from './ChangeMemo.vue';

export default {
  components: {
    IndexMemo, AddMemo, ChangeMemo
  },
  data() {
    return {
      isEditing: false,
      newMemo: '',
      selectedId: null,
      memos: [],
    }
  },
  methods: {
    addMemo(memo) {
      const memoID = Math.random().toString(32).substring(2)
      var newMemo = {
        item: memo,
        id: memoID
      }
      this.memos.push(newMemo)
      this.saveMemo()
    },
    editMemo(index) {
      this.isEditing = true
      this.newMemo = this.memos[index].item
      this.selectedId = this.memos[index].id
      this.selectedIndex = index
    },
    deleteMemo(index) {
      this.memos.splice(this.selectedIndex, 1)
      this.saveMemo()
      this.newMemo = ''
      this.isEditing = false
      this.selectedId = null
    },
    updateMemo(memo) {
      var newMemo = {
        item: memo,
        id: this.selectedId,
      }
      this.memos.splice(this.selectedIndex, 1, newMemo)
      this.saveMemo()
      this.newMemo = ''
      this.isEditing = false
      this.selectedId = null
    },
    saveMemo() {
       localStorage.setItem("memos", JSON.stringify(this.memos))
    }
  },
  mounted() {
    if (localStorage.getItem("memos")) {
      try {
        this.memos = JSON.parse(localStorage.getItem("memos"));
      }catch (e) {
        localStorage.removeItem("memos");
      }
    }
  }
};
</script>

<style>
.container {
  margin: 30px auto;
  width: 600px;
}

h1 {
  color: #2e99a9;
  margin-left: 80px;
}

ul {
  list-style-type: none;
  color: #17A2B8;
  font-size: 25px;
  text-decoration: underline;
}

.left-side {
  float: left;
  margin-left: 80px;
}

.right-side {
  float: right;
  margin-right: 80px;
}
</style>
