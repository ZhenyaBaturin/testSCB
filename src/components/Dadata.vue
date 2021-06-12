<template>
  <div id="app">
    <vue-dadata token="token"></vue-dadata>
  </div>
</template>

<script>
import VueDadata from 'vue-dadata'
 
export default {
  name: 'VueDadataTest',
  components: {
    'vue-dadata': VueDadata
  },
  data() {
      return {
        token: '92d9480112e42f8b923c3ad8ea5af68c46222760'
      }
  }
}
</script> 