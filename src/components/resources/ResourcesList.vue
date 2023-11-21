<template>
  <ul>
    <ResourceItem
      v-for="{ id, title, description, link } in storedResources"
      :title="title"
      :description="description"
      :link="link"
      :key="id"
      :id="id"
    />
  </ul>
</template>

<script>
import ResourceItem from "./ResourceItem.vue";
export default {
  inject: ["storedResources"],
  components: { ResourceItem },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
