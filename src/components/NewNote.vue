<template>
  <!--add note-->
  <div class="new-note">
    <label>Title</label>
    <input v-model="note.title" type="text" />
    <label>Select note priority</label>
    <select v-model="note.selectPriotity">
      <option selected value="default-priority">Default priority</option>
      <option value="low-priority">Low priority</option>
      <option value="high-priority">High Priority</option>
    </select>
    <label>Description</label>
    <textarea v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">Add note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    },
  },
};
</script>

<style lang="scss">
.new-note {
  text-align: center;
  select {
    width: 100%;
    border-radius: 20px;
    padding: 16px 26px;
  }
}
</style>