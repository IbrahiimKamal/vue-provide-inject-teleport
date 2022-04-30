<template>
  <base-card>
    <base-button
      :mod="storedResButtonMode"
      @click="setSelectTab('stored-resources')"
      >Stored Resources</base-button
    >
    <base-button :mod="addResButtonMode" @click="setSelectTab('add-resource')"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import BaseCard from '../UI/BaseCard.vue';
import BaseButton from '../UI/BaseButton.vue';
import StoredResources from './StoredResources.vue';
import AddResource from './AddResources.vue';

export default {
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 1,
          title: 'React',
          description: 'A JavaScript library for building user interfaces.',
          link: 'https://vuejs.org/',
        },
        {
          id: 2,
          title: 'Vuex',
          description: 'A state management library for Vue.js',
          link: 'https://vuex.vuejs.org/',
        },
      ],
    };
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
    };
  },

  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },

  methods: {
    setSelectTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, link) {
      const newResource = {
        id: this.storedResources.length + 1,
        title,
        description,
        link,
      };

      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resource) {
      const index = this.storedResources.findIndex(
        (item) => item.id === resource.id
      );
      this.storedResources.splice(index, 1);
    },
  },

  components: { BaseCard, BaseButton, StoredResources, AddResource },
};
</script>
