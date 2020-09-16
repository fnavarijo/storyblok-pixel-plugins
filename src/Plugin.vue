<template>
  <div class="pixel-list">
    <ol class="pixel-list__list uk-margin-bottom-remove">
      <li
        v-for="(item, index) in model.items"
        :key="index"
        class="pixel-list__list-item uk-flex uk-flex-middle"
      >
        <input
          v-model="model.items[index]"
          class="uk-form-small uk-width-1-1"
          :aria-label="`List item ${index}`"
        >
        <a
          class="assets__item-trash"
          aria-label="Remove item"
          @click="removeItem(index)"
        >
          <i class="uk-icon-minus-circle"></i>
        </a>
      </li>
    </ol>
    <a class="blok__full-btn uk-margin-small-top" @click="addItem">
      <i class="uk-icon-plus-circle uk-margin-small-right" />
      Add Item
    </a>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  methods: {
    initWith() {
      return {
        plugin: 'pixel-list',
        items: [''],
      }
    },
    pluginCreated() {
      // eslint-disable-next-line
      console.log('View source and customize: https://github.com/storyblok/storyblok-fieldtype')
    },
    addItem() {
      this.model.items.push('');
    },
    removeItem(index) {
      this.model.items = this.model.items.filter((_, i) => i !== index);
    }
  },
  watch: {
    model: {
      deep: true,
      handler (value) {
        this.$emit('changed-model', value);
      },
    }
  }
}
</script>

<style>
  .pixel-list {
    padding-left: 0;
  }

  .pixel-list__list-item {
    list-style-type: none;
  }

  .pixel-list__list-item + .pixel-list__list-item {
    margin-top: 5px;
  }
</style>
