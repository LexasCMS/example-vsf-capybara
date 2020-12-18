<template>
  <component :is="section.type" :section="section" />
</template>

<script>
import bestSellers from './section/best-sellers';
import featuredCategories from './section/featured-categories';
import instagramGallery from './section/instagram-gallery';
import newsletterSignup from './section/newsletter-signup';
import promoBanner from './section/promo-banner';

export default {
  components: {
    bestSellers,
    featuredCategories,
    instagramGallery,
    newsletterSignup,
    promoBanner
  },

  props: {
    section: {
      type: Object,
      required: true
    }
  }
}
</script>
