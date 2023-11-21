<template>
  <div>
    <base-card>
      <base-button
        @click="setSelectedTab('ResourcesList')"
        :mode="storedResButtonMode"
        >Stored Resources</base-button
      >
      <base-button
        @click="setSelectedTab('AddResource')"
        :mode="addResButtonMode"
        >Add Resource</base-button
      >
    </base-card>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import ResourcesList from "./ResourcesList.vue";
import AddResource from "./AddResource.vue";
export default {
  components: { ResourcesList, AddResource },
  data() {
    return {
      selectedTab: "ResourcesList",
      storedResources: [
        {
          id: "1",
          title: "Official Guide",
          description: "The official Vue.js documentation",
          link: "https://vuejs.org",
        },
        {
          id: "2",
          title: "Official Guide",
          description: "The official React documentation",
          link: "https://react.dev/",
        },
      ],
    };
  },
  provide() {
    return {
      storedResources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === "ResourcesList" ? null : "flat";
    },
    addResButtonMode() {
      return this.selectedTab === "AddResource" ? null : "flat";
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, link) {
      const newResorce = {
        id: new Date().toISOString(),
        title,
        description,
        link,
      };

      this.storedResources.unshift(newResorce);
      this.selectedTab = "ResourcesList";

    },
    removeResource(resourceId) {
      const resourceIndex = this.storedResources.findIndex(
        ({ id }) => id === resourceId
      );
      this.storedResources.splice(resourceIndex, 1);
    },
  },
};
</script>
