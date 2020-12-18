<template>
  <div v-if="collection[0] !== undefined">
    <ContentPageSection
      v-for="section in collection[0].sections"
      :key="section.id"
      :section="section"
    />
  </div>
</template>

<script>
import LexascmsCollectionMixin from 'src/modules/vsf-lexascms/src/mixins/LexascmsCollection';
import ContentPageSection from './content-page/section';

export default {
  mixins: [ LexascmsCollectionMixin ],

  components: {
    ContentPageSection
  },

  props: {
    contentType: {
      type: String,
      default: 'contentPage'
    }
  }
}
</script>
