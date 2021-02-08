<template>
  <div class="addNote">
    <label for="title">Title
      <input type="text"
        v-model="currentNote.name"
        id="title"
      />
    </label>
    <label for="content">Note
      <textarea
        v-model="currentNote.content"
        id="content"
      />
    </label>
    <div v-if="editIsOn">
      <button
        @click="updateNote(currentNote)">Save Changes</button>
      <button
        @click="editModeToggle()"
      >New Note</button>
    </div>
    <div v-else>
      <font-awesome-icon
        icon="plus-square"
        @click="addNote(currentNote)"
        :class="[currentNote.name && currentNote.content ? 'active' : 'inactive', 'plus']"
      />
    </div>

  </div>
</template>

<script>
export default {
  props: {
    editIsOn: Boolean,
    currentNote: {}
  },
  methods: {
    editModeToggle() {
      this.$emit('turnOffEdit');
    },
    addNote(currentNote) {
      if (currentNote.name == '' && currentNote.content == '') {
        return;
      }
      axios.post('api/item/store', {
        item: currentNote
      })
      .then(response => {
        if (response.status == 201) {
          this.$emit('reloadlist');
          this.editModeToggle();
        }
      })
      .catch(err => {
        console.log(err);
      })
    },
    updateNote(currentNote) {
      axios.put('api/item/' + currentNote.id, {
        item: currentNote
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
  }
}
</script>

<style scoped>
.addNote {
  display: grid;
  margin: 0 auto;
  grid-template-rows: 1fr 5fr 1fr;
  border: 1px white solid;
  width: 100%;
}
input, textarea {
  background: #f7f7f7;
  border: 0px;
  outline: none;
  padding: 0px;
  margin: 10px 0;
  width: 100%;
}
.plus {
  font-size: 20px;
}
.active {
  color: #00CE25;
}
.inactive {
  color: #999999;
}
</style>