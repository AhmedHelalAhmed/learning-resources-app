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
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
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
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, link) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: link
      };
      // this.storedResources.push(newResource);
      this.storedResources.unshift(newResource); // this not create new array but modify the original
      this.selectedTab = 'stored-resources';
    },
    removeResource(resourceId) {
      /*
      // this will not work since we just assign the refernce to new array
      // and provide not update the other reference
      this.storedResources = this.storedResources.filter(
        resource => resource.id !== resourceId
      );//this create new array
      */

      const resourceIndex = this.storedResources.findIndex(
        resource => resource.id === resourceId
      );

      this.storedResources.splice(resourceIndex, 1); // this not create new array but modify the original
    }
  }
};
</script>
