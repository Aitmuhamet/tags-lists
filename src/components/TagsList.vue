<template>
  <div :class="['tags-list', `tags-list--${alignment}`]" :style="{ fontSize: fontSize + 'px' }">
    <template v-for="(tag, index) in visibleTags">
      <div :key="index"  class="tags-list__tag">
        <v-chip :style="{ fontSize: fontSize + 'px' }">
          <v-icon v-if="tag.icon" :class="['tags-list__icon', tag.icon]">{{ tag.icon }}</v-icon>
          {{ tag.text }}
        </v-chip>
        <v-icon v-if="index < visibleTags.length - 1" class="tags-list__separator">mdi-circle-small</v-icon>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'TagsList',
  props: {
    tags: {
      type: Array,
      required: true,
      default: () => []
    },
    alignment: {
      type: String,
      default: 'left',
      validator: value => ['left', 'justify'].includes(value)
    },
    fontSize: {
      type: Number,
      required: true,
      default: 16
    }
  },
  watch: {
    fontSizeBlock: function(newVal, oldVal) {
      console.log(newVal, oldVal);
    }
  },
  data() {
    return {
      visibleTags: [],
      fontSizeBlock: this.fontSize,
    }
  },
  mounted() {
    this.updateVisibleTags();
    window.addEventListener('resize', this.updateVisibleTags);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.updateVisibleTags);
  },
  methods: {
    updateFontSize(newSize) {
      this.fontSizeBlock = newSize;
    },
    updateVisibleTags() {
      const containerWidth = this.$el.clientWidth;
      console.log('It works')
      
      let currentWidth = 0;
      this.visibleTags = [];
      
      console.log(this.tags);

      this.tags.forEach(tag => {
        const tagWidth = this.getTagWidth(tag);
        console.log(tagWidth);
        if (currentWidth + 32 + tagWidth <= containerWidth) {
          this.visibleTags.push(tag);
          currentWidth += 32;
          currentWidth += tagWidth;
        }
      });
    },
    getTagWidth(tag) {
      // Создаем временный элемент для вычисления ширины
      const tempElement = document.createElement('div');
      tempElement.className = 'tags-list__tag';
      tempElement.style.visibility = 'hidden';
      tempElement.style.position = 'absolute';
      tempElement.innerText = tag.text;
      document.body.appendChild(tempElement);
      console.log('It`s work!');

      let width = tempElement.clientWidth + 24;
      if (tag.icon) {
        width += 24;
      }
      document.body.removeChild(tempElement);
      return width;
    }
  }
}
</script>

<style lang="scss">
.tags-list {
  display: flex;
  align-items: stretch;
  border: 1px solid #c6d2d0;
  border-radius: 16px;
  margin: 10px 0;
  &__tag {
    display: flex;
    justify-content: start;
  }

  &__tag,
  .v-chip,
  .v-chip__content  {
    margin-right: 0px;
    font-size: unset !important;
    line-height: unset;
    height: unset;
    // min-height: 100%;
  }
  &__separator {
    margin: 0 4px;
  }
  &--justify {
    justify-content: space-between;

    .tags-list__tag:not(:last-child) {
      flex: 1;
    }

    .v-icon {
      margin: 0 auto;
    }
  }
  .v-chip,
  .v-chip__content {

  }
}
</style>
