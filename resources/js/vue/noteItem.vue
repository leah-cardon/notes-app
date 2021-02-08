<template>
  <div class="item">
    <div class="titleText">{{ item.name }}</div>
    <button :item="item" @click="editModeToggle(item)" class="edit">
      <font-awesome-icon icon="edit" />
    </button>
    <button @click="deleteNote()" class="trashcan">
      <font-awesome-icon icon="trash" />
    </button>
  </div>
</template>

<script>
export default {
  props: ['item'],
  methods: {
    editModeToggle(item) {
      this.$emit('editIsOn', item);
    },
    deleteNote() {
      axios.delete('api/item/' + this.item.id)
      .then(response => {
        if (response.status == 200) {
          this.$emit('itemchanged');
        }
      })
      .catch(err => {
        console.log(err);
      })
    }
  }
}
</script>

<style scoped>
.titleText {
  font-size: 25px;
  font-family: 'Arial';
}
.noteText {
  font-size: 12px;
  font-family: 'Arial';
}
.item {
  display: flex;
  justify-content: center;
  align-items: center;
}
.edit {
  background: #e6e6e6;
  border: none;
  color: black;
  outline: none;
}
.trashcan {
  background: #e6e6e6;
  border: none;
  color: #FF0000;
  outline: none;
}
</style>