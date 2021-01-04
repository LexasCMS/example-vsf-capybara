<template>
  <div id="app">
    <div id="example-app-banner">
      <span>
        This is an e-commerce store example built with
        <a href="https://www.lexascms.com/vue-storefront/" target="_blank">LexasCMS</a> and
        <a href="https://www.vuestorefront.io/" target="_blank">Vue Storefront 1.x</a> -
        <a href="https://github.com/lexascms/example-vsf-capybara/" target="_blank">View source code</a>
      </span>
    </div>
    <component :is="layout">
      <router-view />
    </component>
  </div>
</template>

<script>
import get from 'lodash-es/get'
import DefaultLayout from './layouts/Default'
import MinimalLayout from './layouts/Minimal'

export default {
  components: {
    DefaultLayout,
    MinimalLayout
  },
  computed: {
    layout () {
      return `${get(this.$route, 'meta.layout', 'default')}-layout`
    }
  }
};
</script>

<style lang="scss" src="theme/css/main.scss"></style>
<style lang="scss">
@import "~@storefront-ui/shared/styles/helpers/breakpoints";
body {
  --overlay-z-index: 1;
  --sidebar-aside-z-index: 2;
  --bottom-navigation-height: 3.75rem;
  --bar-height: 3.125rem;
  --notification-font-size: var(--font-sm);
  font-family: var(--font-family-secondary);
  margin: 0;
  padding: 0;
  a {
    text-decoration: none;
    color: var(--c-link);
    cursor: pointer;
    &:hover {
      color: var(--c-link-hover);
    }
  }
}

#example-app-banner {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #1a202c;
  color: #e2e8f0;
  font-size: 14px;
  padding: 14px 16px;

  a {
    color: inherit;
    text-decoration: underline;
  }
}

#viewport {
  position: relative;
}

@include for-desktop {
  .sidebar {
    &__microcart {
      --sidebar-aside-width: 700px;
    }
  }
}
</style>
