<template>
  <div>
    <button
      v-if="cards.length > 1"
      @click="toggleCollapse"
      class="md:hidden h-8 py-3 mb-3 uppercase tracking-widest font-bold text-xs inline-flex items-center justify-center focus:outline-none focus:ring-primary-200 border-1 border-primary-500 focus:ring focus:ring-offset-4 focus:ring-offset-gray-100 dark:ring-gray-600 dark:focus:ring-offset-gray-900 rounded"
    >
      <span>{{ collapsed ? __("Show Cards") : __("Hide Cards") }}</span>
      <CollapseButton class="ml-1" :collapsed="collapsed" />
    </button>

    <div v-if="cards.length > 0" class="grid md:grid-cols-12 gap-6">
      <CardWrapper
        v-show="!collapsed"
        v-for="card in cards"
        :card="card"
        :resource="resource"
        :resource-name="resourceName"
        :resource-id="resourceId"
        :key="`${card.component}.${card.uriKey}`"
        :lens="lens"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cards: Array,

    resource: {
      type: Object,
      required: false,
    },

    resourceName: {
      type: String,
      default: "",
    },

    resourceId: {
      type: [Number, String],
      default: "",
    },

    onlyOnDetail: {
      type: Boolean,
      default: false,
    },

    lens: {
      lens: String,
      default: "",
    },
  },

  data: () => ({ collapsed: false }),

  computed: {
    localStorageKey() {
      return `nova.cards.${this.resource}.${this.size}.collapsed`;
    },
  },
};
</script>
