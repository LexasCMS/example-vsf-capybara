<template>
  <SfSection :title-heading="section.title" class="section">
    <lazy-hydrate :trigger-hydration="!loading">
      <m-product-carousel :products="newCollection" />
    </lazy-hydrate>
  </SfSection>
</template>

<script>
import { mapGetters } from 'vuex';
import LazyHydrate from 'vue-lazy-hydration'
import { isServer } from '@vue-storefront/core/helpers';
import MProductCarousel from '../../molecules/m-product-carousel';

import {
  SfSection
} from '@storefront-ui/vue';

export default {
  components: {
    LazyHydrate,
    MProductCarousel,
    SfSection
  },

  props: {
    section: {
      type: Object,
      required: true
    }
  },

  computed: {
    ...mapGetters({
      newCollection: 'homepage/getEverythingNewCollection'
    })
  },

  data () {
    return {
      loading: true
    };
  },

  watch: {
    newCollection () {
      this.loading = false;
    }
  }
}
</script>
