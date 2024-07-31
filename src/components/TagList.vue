<template>
  <div ref="containerRef" class="tag-list">
    <v-row class="tag-list__row" :justify="alignment">
      <div v-for="(tag, index) in visibleTags" :key="tag.id">
        <v-col class="tag-list__tag" :cols="getColSize(tag)">
          {{ tag.text }}
          <v-icon v-if="index < visibleTags.length - 1" class="tag-list__icon" small>
            {{ tag.icon }}
          </v-icon>
        </v-col>
      </div>
    </v-row>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted, watch } from 'vue';
import { useResizeObserver } from '@vueuse/core';
import {debounce} from '@/useApi/debonce'; // Assuming debounce is correctly exported

export default defineComponent({
  name: 'TagList',
  props: {
    tags: {
      type: Array,
      required: true,
    },
    alignment: {
      type: String,
      default: 'start',
    },
  },
  setup(props) {
    const containerRef = ref(null);
    const visibleTags = ref([]);

    const getColSize = () => {
      return Math.floor(24 / props.tags.length);
    };

    const calculateVisibleTags = () => {
      if (!containerRef.value) return;

      const containerWidth = containerRef.value.offsetWidth;
      let totalWidth = 0;
      visibleTags.value = [];

      for (const tag of props.tags) {
        const tagWidth = getColSize(tag) * 10;
        totalWidth += tagWidth;

        if (totalWidth > containerWidth) break;
        visibleTags.value.push(tag);
      }
    };

    const debouncedCalculateVisibleTags = debounce(calculateVisibleTags, 200);

    onMounted(() => {
      calculateVisibleTags();
    });

    useResizeObserver(containerRef, debouncedCalculateVisibleTags);

    watch(() => props.tags, calculateVisibleTags);

    return {
      containerRef,
      visibleTags,
      getColSize,
    };
  },
});
</script>

<style lang="scss" scoped>
.tag-list {
  padding: 20px 0;
  &__row {
    display: flex;
    flex-wrap: nowrap;
  }
  &__tag {
    text-align: center;
  }
  &__icon {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>