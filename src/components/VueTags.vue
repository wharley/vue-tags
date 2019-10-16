<template>
  <div>
    <div class="tag-wrapper">
      <input
        v-model="tag"
        @input="getFilter"
      />
      <ul v-show="isOpen" class="tag-ul-autocomplete">
        <li
          v-for="tag in results"
          :key="tag"
          class="tag-li-autocomplete"
          @click="appendTag(tag)"
        >
          {{ tag }}
        </li>
      </ul>
    </div>
    <div class="tag-list-wrapper">
      <span v-for="tag in tags" :key="tag" class="tag-list">
        {{ tag }}
        <span class="tag-remove" @click="removeTag(tag)">
          &times;
        </span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueTag',
  props: {
    tags: {
      type: Array,
      default: () => []
    },
    suggestions: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      tag: '',
      isOpen: false,
      results: [],
      newTags: []
    }
  },
  methods: {
    getFilter() {
      if (this.tag !== '') {
        this.results = this.suggestions.filter(tag => tag.toLowerCase().indexOf(this.tag.toLowerCase()) === 0)
        this.isOpen = true;
      } else {
        this.results = [];
        this.isOpen = false;
      }
    },
    appendTag(item) {
      this.tag = '';
      this.isOpen = false;
      if (item.trim() === '') return;

      let duplicate = false;
      this.newTags.forEach((tag) => {
        if (tag === item.trim()) {
          duplicate = true;
        }
      });

      if (duplicate) return;

      this.newTags.push(item.trim());
      this.$emit('tags-changed', this.newTags);
    },
    removeTag(tag) {
      const index = this.newTags.indexOf(tag);
      this.newTags.splice(index, 1);
      this.$emit('tags-changed', this.newTags);
    }
  }
}
</script>

<style lang="scss" scoped>
.tag-wrapper {
  width: 100%;
  position: relative;
  display: inline-block;

  > input {
    outline: none;
    width: 192px;
    height: 25px;

    border: solid 2px #E8E8E8;
    border-radius: 9px;

    &:focus {
      border-bottom: 2px solid #26a69a;
    }
  }
}

.tag-ul-autocomplete {
  margin: 0;
  padding: 0;
  width: 200px;

  border-radius: 9px;
  box-shadow: .05em .01em .5em rgba(0,0,0,.2);
  background: white;
  list-style-type: none;
}

.tag-li-autocomplete {
  padding: 5px 10px;
  margin: 0;
  text-align: left;

  list-style: none;
  border-bottom: 1px solid #ddd;
  cursor: pointer;

  &:hover {
    background-color: #D3D3D3;
  }
}

.tag-list-wrapper {
  font-family: Roboto, sans-serif;
  font-size: 11.8px;
  letter-spacing: 1.25px;

  padding: 10px 0;
  max-width: 450px;
}

.tag-list {
  display: inline-block;
  padding: 5px 5px 5px 10px;
  margin: 5px 5px 5px 0;

  background: #d8d8d8;
  font-size: 14px;
  border-radius: 20px;
  cursor: pointer;
}

.tag-remove {
  display: inline-block;
  width: 15px;
  margin-left: 5px;

  background-color: #9b9a9b;
  border-radius: 99px;
  line-height: 15px;
  font-size: 15px;
  text-align: center;
  color: #d8d8d8;
  cursor: pointer;
}
</style>

