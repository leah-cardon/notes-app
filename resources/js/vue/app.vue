<template>
  <div class="notesListContainer">
    <div class="heading">
      <h2 id="title">Notes</h2>
    </div>
    <div class="listAndForm">
      <notes-view
        :items="items"
        v-on:reloadlist="getNotes()"
        v-on:turnOnEdit="toggleEdit(true, $event)"
      />
      <!-- if edit mode is on, display title and content fields with a save button and a button to switch back to new note -->
      <!-- if it's off (by default), show the new note form which includes the + -->
      <add-note-form
        :edit-is-on="editIsOn"
        v-on:reloadlist="getNotes()"
        v-on:turnOffEdit="toggleEdit(false, null)"
      />
    </div>
  </div>
</template>

<script>
  import addNoteForm from "./addNoteForm";
  import notesView from "./notesView";
  export default {
    components: {
      addNoteForm,
      notesView
    },
    data: function () {
      return {
        items: [],
        currentNote: {},
        editIsOn: false
      }
    },
    methods: {
      toggleEdit(bool, item) {
        this.editIsOn = bool;
        if (item) {
          this.currentNote = item;
          console.log(this.currentNote, 'added to state');
        }
        this.$forceUpdate();
      },
      getNotes() {
        axios.get('api/items')
        .then(response => {
          this.items = response.data
        })
        .catch(err => {
          console.log(err);
        })
      }
    },
    created() {
      this.getNotes();
    }

  }
</script>

<style scoped>
  .notesListContainer {
    width: 60%;
    margin: auto;
    display: grid;
  }
  .heading {
    background: #e6e6e6;
    padding: 10px;
  }
  #title {
    text-align: center;
  }
  .listAndForm {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
</style>