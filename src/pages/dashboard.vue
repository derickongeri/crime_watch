<template>
  <q-page class="page-body">
    <div
      class="row justify-center"
      style="position: absolute; z-index: 5000; top: 0%; left: 20%"
    >
      <crimeTabs />
    </div>

    <Mappanel />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    Mappanel: require("components/Map/Map.vue").default,
    crimeTabs: require("components/Selections/crimetabs.vue").default,
  },

  setup() {},
});
</script>

<style scoped>
.page-body {
  background-image: url("~/src/assets/3387682.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  box-shadow: inset 0px 0px 50vw 16vh rgba(0, 0, 0, 0.5);
}
</style>
