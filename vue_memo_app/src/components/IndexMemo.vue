<template>
  <div>
    <ul>
      <li v-for="(memo, index) in memos" v-bind:key="memo.id">
        <a @click="editMemo(index)">
          {{ memo.item.split('\n')[0] }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['memos'],
  data() {
    return {
      isEditing: false,
      isAdding: false
    }
  },
  methods: {
    editMemo(index) {
      this.$emit('edit-memo', index);
    }
  }
};
</script>
