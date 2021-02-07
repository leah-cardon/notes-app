<template>
  <div>
    <div f-for="(item, index) in items" :key="index" >
      <list-item
        :item="item"
        class="item"
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