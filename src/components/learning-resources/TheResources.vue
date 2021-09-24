<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResourcesButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="AddResourceButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: { StoredResources, AddResource },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org'
        }
      ]
    };
  },
  computed: {
    storedResourcesButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    AddResourceButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  provide() {
    return { resources: this.storedResources };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    }
  }
};
</script>
