# vue-tags-custom

![Screenshot of Vue Tags](src/assets/vue-tags.gif)

A fantastically simple tagging component for your Vue projects

### Installation

```
npm install --save vue-tags-custom
```

Or

```
yarn add vue-tags-custom
```

### Usage

Here's a sample implementation that initializes the component with a list of initial `tags` and `suggestions` list.

```html
<template>
  <div>
    <VueTags
      :suggestions="tagList"
      :tags="tags"
      @tags-changed="newTags => tags = newTags"
    />
  </div>
</template>
```

```javascript
<script>
import VueTags from 'vue-tags-custom'

export default {
  name: 'app',
  components: {
    VueTags
  },
  data() {
    return {
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
```


## License

[MIT](https://opensource.org/licenses/MIT)

