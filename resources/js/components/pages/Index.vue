<template>
  <div>
    <LoadingView :loading="loading">
      <ResourceCards
        v-if="shouldShowIndexCards"
        :cards="indexCards"
        :resource="resource"
        :resource-name="resourceName"
        class="mb-6 resource-cards"
      />
    </LoadingView>
    <OriginalIndexPage v-bind="$props" />
  </div>
</template>

<script>
import HasCards from "#/mixins/HasCards";
export default {
  mixins: [HasCards],
  components: {
    OriginalIndexPage: Nova.pages["Original.Nova.Index"],
  },
  extends: Nova.pages["Original.Nova.Index"],
  inheritAttrs: false,

  computed: {
    cardsEndpoint() {
      return `/nova-vendor/resource-cards/${this.resourceName}/cards`;
    },

    extraCardParams() {
      return {
        resourceName: this.resourceName,
        display: "index",
      };
    },
  },
};
</script>
