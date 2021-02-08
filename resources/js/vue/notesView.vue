<template>
  <div>
    <div v-for="(item, index) in items" :key="index" >
      <note-item
        :item="item"
        class="item"
        v-on:itemchanged="$emit('reloadlist')"
        v-on:editIsOn="$emit('turnOnEdit')"
      />
    </div>
  </div>
</template>

<!-- add click event handler in note-item above that puts the right item into state as the current item, and move itemchanged event to form component -->

<script>
import noteItem from './noteItem'

export default {
  props: ['items'],
  components: {
    noteItem
  }
}
</script>

<style scoped>
.item {
  background: #e6e6e6;
  padding: 5px;
  margin-top: 5px;
}
</style>