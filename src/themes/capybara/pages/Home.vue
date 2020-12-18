<template>
  <div id="home">
    <ContentPage
      :filter="{
        slug: {
          _eq: 'homepage'
        }
      }"
      :page="{
        limit: 1,
        sections: {
          limit: 5,
          bannerItems: {
            limit: 5
          },
          featuredCategories: {
            limit: 4
          }
        }
      }"
      :include="include"
    />
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import { Logger } from '@vue-storefront/core/lib/logger';
import { isServer } from '@vue-storefront/core/helpers';
import ContentPage from 'theme/components/content-page';

export default {
  name: 'Home',
  components: {
    ContentPage
  },
  data () {
    return {
      include: 'sections,' + // Content Page Sections
               'sections.bannerItems,sections.bannerItems.backgroundImage,' + // Promo Banner Items
               'sections.featuredCategories,sections.featuredCategories.backgroundImage,' + // Featured Categories
               'sections.backgroundImage', // Newsletter Signup
      loadNewsletterPopup: false
    };
  },
  computed: {
    ...mapGetters({
      isLoggedIn: 'user/isLoggedIn'
    })
  },
  watch: {
    isLoggedIn () {
      const redirectObj = localStorage.getItem('redirect');
      if (redirectObj) this.$router.push(redirectObj);
      localStorage.removeItem('redirect');
    }
  },
  async asyncData ({ store, context }) {
    Logger.info('Calling asyncData in Home (theme)')();
    if (context) context.output.cacheTags.add(`home`)

    await Promise.all([
      store.dispatch('homepage/fetchNewCollection'),
      store.dispatch('promoted/updateHeadImage'),
      store.dispatch('instagram/updateInstagramImages')
    ]);
  },
  mounted () {
    if (!this.isLoggedIn && localStorage.getItem('redirect')) { this.$bus.$emit('modal-show', 'modal-signup'); }
  },
  beforeRouteEnter (to, from, next) {
    if (!isServer && !from.name) {
      next(vm => {
        vm.$store.dispatch('homepage/fetchNewCollection').then(() => {
          vm.loading = false;
        });
      });
    } else {
      next();
    }
  },
  metaInfo () {
    return {
      title: this.$route.meta.title || this.$i18n.t('Home Page'),
      meta: this.$route.meta.description ? [{ vmid: 'description', name: 'description', content: this.$route.meta.description }] : []
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~@storefront-ui/shared/styles/helpers/breakpoints";

#home {
  box-sizing: border-box;
  padding: 0 var(--spacer-sm);
  @include for-desktop {
    padding: 0 var(--spacer-sm);
    max-width: 1272px;
    margin: 0 auto;
  }
}
.sf-hero-item {
  --hero-item-height: 14rem;
  height: initial;
}
.section {
  @include for-desktop {
    padding-left: 0;
    padding-right: 0;
  }
}
</style>
