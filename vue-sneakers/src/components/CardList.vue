<script setup>

defineProps({
  items: Array,
})
import Card from './Card.vue'


</script>
<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
        :key="item.id"
        :title="item.title"
        :image-url="item.imageUrl"
        :price="item.price"
        :on-click-add="onClickAdd"
    />

  </div>
</template>
