<template>
  <div id="app">
    <h5>What countries have you visited?</h5>
    <VueTags
      :suggestions="tagList"
      :tags="tags"
      @tags-changed="newTags => tags = newTags"
    />
  </div>
</template>

<script>
import VueTags from '@/components/VueTags.vue'

export default {
  name: 'app',
  components: {
    VueTags
  },
  data() {
    return {
      tag: '',
      tagList: [
        'Georgia',
        'Germany',
        'Gifu',
        'India',
        'Thailand',
        'Tóquio',
        'Russia'
      ],
      tags: []
    }
  }
}
</script>
