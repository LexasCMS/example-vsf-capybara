<template>
  <ONewsletter
    :title="section.title"
    :description="section.subtitle"
    :button-text="section.buttonText"
    :background-image="section.backgroundImage.url"
  />
</template>

<script>
import ONewsletter from '../../organisms/o-newsletter';

export default {
  components: {
    ONewsletter
  },

  props: {
    section: {
      type: Object,
      required: true
    }
  }
}
</script>
