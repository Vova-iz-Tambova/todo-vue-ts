<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        class="button"
        :class="{ 'button--primary': activeFilter === filter }"
        @click="setFiler(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import { Filter } from "@/types/Filter";
import { PropType, defineComponent } from "vue";

interface State {
  filters: Filter[];
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
    },
  },
  data(): State {
    return {
      filters: ["All", "Active", "Done"],
    };
  },
  methods: {
    setFiler(filter: Filter) {
      this.$emit("setFiler", filter);
    },
  },
  emits: {
    setFiler: (filter: Filter) => filter,
  },
});
</script>
