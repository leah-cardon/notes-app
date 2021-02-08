<template>
  <div class="item">
    <div class="titleText">{{ item.name }}</div>
    <div class="noteText">{{ item.content }}</div>
    <!-- CHANGE THIS:
    edit button opens the text for editing
    a save button sends the updateNote (put request) -->
    <button @click="updateNote()" class="edit">
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
    updateNote() {
      axios.put('api/item/' + this.item.id, {
        item: this.item
      })
      .then(response => {
        if (response.status == 200) {
          this.$emit('itemchanged');
        }
      })
      .catch(err => {
        console.log(err);
      });
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
  font-size: 40px;
}
.noteText {
  font-size: 12px;
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