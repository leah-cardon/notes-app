<template>
  <div class="addNote">
    <label for="title">Title
      <input type="text"
        v-model="item.name"
        id="title"
        value="item.name"
      />
    </label>
    <label for="content">Note
      <textarea
        v-model="item.content"
        id="content"
        value="item.content"
      />
    </label>
    <div v-if="editIsOn">
      <button>Save Changes</button>
      <button
        @click="editModeToggle()"
      >New Note</button>
    </div>
    <div v-else>
      <font-awesome-icon
        icon="plus-square"
        @click="addNote()"
        :class="[item.name && item.content ? 'active' : 'inactive', 'plus']"
      />
    </div>

  </div>
</template>

<script>
export default {
  data: function () {
    return {
      item: {
        name: '',
        content: ''
      }
    }
  },
  props: {
    editIsOn: Boolean
  },
  methods: {
    editModeToggle() {
      this.$emit('turnOffEdit');
    },
    addNote() {
      if (this.item.name == '' && this.item.content == '') {
        return;
      }

      axios.post('api/item/store', {
        item: this.item
      })
      .then(response => {
        if (response.status == 201) {
          this.item.name = '';
          this.item.content = '';
          this.$emit('reloadlist');
        }
      })
      .catch(err => {
        console.log(err);
      })
    },
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