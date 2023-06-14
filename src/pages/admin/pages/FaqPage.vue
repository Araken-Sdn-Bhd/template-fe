<template>
  <div class="not-found-pages">
    <div class="row mb-4">
      <va-card class="flex xs12">
        <va-card-title> Do you have any questions? </va-card-title>
        <va-card-content>
          <va-input>
            <template #prepend>
              <va-icon name="search" />
            </template>
          </va-input>
        </va-card-content>
      </va-card>
    </div>
    <div class="row">
      <va-card class="flex xs12">
        <va-card-title> Frequently Asked Questions </va-card-title>
        <va-card-content>
          <va-accordion>
            <va-collapse header="First question">
              <div class="pa-3">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. Nemo veniam provident voluptates consequuntur
                nostrum cumque possimus unde asperiores magnam rem.
              </div>
            </va-collapse>
            <va-collapse header="Second question">
              <div class="pa-3">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. Nemo veniam provident voluptates consequuntur
                nostrum cumque possimus unde asperiores magnam rem.
              </div>
            </va-collapse>
            <va-collapse header="Third question">
              <div class="pa-3">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. Nemo veniam provident voluptates consequuntur
                nostrum cumque possimus unde asperiores magnam rem.
              </div>
            </va-collapse>
            <va-collapse header="Fourth question">
              <div class="pa-3">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. Nemo veniam provident voluptates consequuntur
                nostrum cumque possimus unde asperiores magnam rem.
              </div>
            </va-collapse>
            <va-collapse header="Fifth question">
              <div class="pa-3">
                {{ this.catTags }}
              </div>
            </va-collapse>
          </va-accordion>
        </va-card-content>
      </va-card>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import type { AxiosInstance } from 'axios';

declare module '@vue/runtime-core' {
  interface ComponentCustomProperties {
    $axios: AxiosInstance
    catTags: string[]
  }
}

interface DogBreed {
  name: string
}

export default defineComponent({
  name: 'HomeView',
  data() {
    return {
      catTags: [] as string[],
      displayStart: 0,
      displayCount: 5,
      activeTag: '',
      catImage: '',
    };
  },
  computed: {
  },
  methods: {
    async fetchCatTags() {
      const tagsResponse = await this.$axios.get('tags')
      this.catTags = tagsResponse.data
    },
    selectTag(tag: string) {
      const baseUrl = 'https://cataas.com/'
      this.catImage = `${baseUrl}cat/${tag}`
      this.activeTag = tag
    },
    loadDefaultCatImage() {
      const baseUrl = 'https://cataas.com/'
      this.catImage = `${baseUrl}cat/gif`
    }
  },
  async mounted() {
    await this.fetchCatTags();
  },
});
</script>