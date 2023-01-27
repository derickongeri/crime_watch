<template>
  <q-page class="row page-body">

      <Mappanel/>
    <!-- <div class="col-2"><analysisTabs /></div>
    <div class="col-6"></div>
    <div class="col-4"><analysisTabs/></div> -->
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    Mappanel: require("components/Map/Map.vue").default,
    crimeTabs: require("components/Selections/crimetabs.vue").default,
    analysisTabs: require("components/Analysis/crimeAnalysis.vue").default,
  },

  setup() {},
});
</script>

<style scoped>
.page-body {
  height: 100%;
  background: rgb(0, 0, 0) url("~/src/assets/3387682.jpg") no-repeat center;
  background-size: cover;
  box-shadow: inset 0px 0px 50vw 56vh rgba(0, 0, 0, 0.5);
}
</style>
