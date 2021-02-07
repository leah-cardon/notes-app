<template>
  <div class="addNote">
    <div>
      <input type="text" v-model="item.name" placeholder="Title" />
      <textarea v-model="item.content" placeholder="Note" />
    </div>
    <font-awesome-icon
      icon="plus-square"
      @click="addNote()"
      :class="[item.name && item.content ? 'active' : 'inactive', 'plus']"
    />
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
  methods: {
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
.addNote {
  display: grid;
  margin: 0 auto;
  grid-template-rows: 100px auto;
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