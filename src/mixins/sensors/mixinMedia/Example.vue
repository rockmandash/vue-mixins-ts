<template>
  <div>
    <!-- you can access these property, if you forgot, you can go to component and simply type this.mixin... and you will get all available property -->
    <div>tablet: {{ mixinMedia.tablet }}</div>
    <div>mobile: {{ mixinMedia.mobile }}</div>
  </div>
</template>

<script lang="ts">
import { mixins, mixinMedia } from '../../../'; // replace the path with 'vue-mixins-ts';

const customMixinForTablet = mixinMedia({
  query: '(min-width: 480px)',
  queryName: 'tablet',
});

const customMixinForMobile = mixinMedia({
  query: '(max-width: 480px)',
  queryName: 'mobile',
});
// or
const customMixin2 = mixinMedia({
  query: '(min-width: 480px)',
  queryName: 'tablet',
  defaultState: false,
  onMatchMedia: isMatched => {
    // a custom callback for you
    console.log(isMatched);
  },
  debounce: {
    wait: 300, // provide wait option (by lodash)
  },
  throttle: {
    wait: 300,
    options: {
      // or lodash throttle options
      leading: true,
      trailing: false,
    },
  },
});

export default mixins(
  customMixinForTablet,
  customMixinForMobile
  // you can add multiple mixin provided by 'vue-mixins-ts' here like mixinWindowSize()
).extend({
  // write your normal component here
  mounted() {
    // you can type this.mixin... and TypeScript will show all available mixin data property.
    console.log(this.mixinMedia);
  },
});
</script>
