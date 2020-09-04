<template>
  <div>hellp</div>
  <!-- <div>1234</div> -->
</template>

<script>
import { defineComponent } from "vue";

import {test} from './test.js'
export default defineComponent({
  name: "HelloWorld",
  setup() {
    test()
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
