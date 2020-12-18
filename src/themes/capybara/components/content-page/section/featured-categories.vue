<template>
  <SfBannerGrid :banner-grid="1" class="banner-grid">
    <!-- eslint-disable-next-line vue/no-unused-vars -->
    <template v-for="(featuredCategory, i) in section.featuredCategories" #[bannerGridSlots[i]]>
      <router-link :key="featuredCategory.id" :to="featuredCategory.categoryLink">
        <SfBanner
          :subtitle="featuredCategory.subtitle"
          :title="featuredCategory.title"
          :description="featuredCategory.description"
          :button-text="featuredCategory.buttonText"
          :image="featuredCategory.backgroundImage.url"
        />
      </router-link>
    </template>
  </SfBannerGrid>
</template>

<script>
import {
  SfBannerGrid,
  SfBanner
} from '@storefront-ui/vue';

export default {
  components: {
    SfBannerGrid,
    SfBanner
  },

  props: {
    section: {
      type: Object,
      required: true
    }
  },

  data () {
    return {
      bannerGridSlots: [
        'banner-A',
        'banner-B',
        'banner-C',
        'banner-D'
      ]
    };
  }
}
</script>

<style lang="scss" scoped>
@import "~@storefront-ui/shared/styles/helpers/breakpoints";

.banner-grid {
  margin: var(--spacer-base) 0;
  @include for-desktop {
    margin: var(--spacer-2xl) 0;
  }
}
</style>
