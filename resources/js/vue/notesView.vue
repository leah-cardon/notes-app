<template>
  <div>
    <div v-for="(item, index) in items" :key="index" >
      <note-item
        :item="item"
        class="item"
        <!-- add click event handler here that puts the right item into state as the current item -->
        v-on:itemchanged="$emit('reloadlist')"
      />
    </div>
  </div>
</template>

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