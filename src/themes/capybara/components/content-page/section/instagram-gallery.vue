<template>
  <SfSection
    :title-heading="section.title"
    :subtitle-heading="section.subtitle"
    class="section"
  >
    <AImagesGrid :images="instagramImages" />
  </SfSection>
</template>

<script>
import { mapState, mapGetters } from 'vuex';
import {
  SfSection
} from '@storefront-ui/vue';
import { checkWebpSupport } from 'theme/helpers';
import AImagesGrid from 'theme/components/atoms/a-images-grid';

export default {
  components: {
    AImagesGrid,
    SfSection
  },

  props: {
    section: {
      type: Object,
      required: true
    }
  },

  computed: {
    ...mapState({
      isWebpSupported: state => state.ui.isWebpSupported
    }),
    ...mapGetters({
      dummyInstagramImages: 'instagram/getInstagramImages'
    }),
    instagramImages () {
      return checkWebpSupport(this.dummyInstagramImages, this.isWebpSupported)
    }
  }
}
</script>
