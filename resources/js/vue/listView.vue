<template>
  <div>
    <div v-for="(item, index) in items" :key="index">
      <list-item
        :item="item"
        class="item"
        v-on:itemChanged="$emit('reloadList')"
      />
    </div>
  </div>
</template>

<script>
import listItem from "./listItem.vue";

export default {
  props: ["items"],
  components: {
    listItem,
  },
};
</script>

<style scoped>
.item {
  background: #e5e7eb;
  padding: 5px;
  margin-top: 5px;
  border-radius: 5px;
}
</style>