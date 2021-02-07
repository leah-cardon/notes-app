<template>
  <div class="notesListContainer">
    <div class="heading">
      <h2 id="title">Notes</h2>
      <add-note-form />
    </div>
    <notes-view />

  </div>
</template>

<script>
  import addNoteForm from "./addNoteForm";
  import notesView from "./notesView";
  export default {
    components: {
      addNoteForm,
      notesView
    }

  }
</script>

<style scoped>
  .notesListContainer {
    width: 350px;
    margin: auto;
  }

  .heading {
    background: #e6e6e6;
    padding: 10px;
  }

  #title {
    text-align: center;
  }
</style>