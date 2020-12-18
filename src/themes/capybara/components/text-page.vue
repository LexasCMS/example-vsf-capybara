<template>
  <div v-if="collection[0] !== undefined">
    <AStatic :content="collection[0]" />
  </div>
</template>

<script>
import LexascmsCollectionMixin from 'src/modules/vsf-lexascms/src/mixins/LexascmsCollection';
import AStatic from './atoms/a-static';

export default {
  mixins: [ LexascmsCollectionMixin ],

  components: {
    AStatic
  },

  props: {
    contentType: {
      type: String,
      default: 'textPage'
    }
  }
}
</script>
