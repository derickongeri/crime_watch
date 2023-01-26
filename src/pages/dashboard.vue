<template>
  <q-page class="row page-body">
    <div class="col-3" style="">selections</div>
    <div class="col">
      <div class="row" style="width:100%;height:15%;"></div>
      <div class="row" style="width:100%;height:60%"><Mappanel/></div>
      <div class="row" style="width:100%;height:25%;"></div>
      </div>
    <div class="col-4" style="">charts</div>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  components: {
    Mappanel: require("components/Map/Map.vue").default,
  },

  setup() {

  },
})
</script>

<style scoped>

.page-body{
  box-shadow: inset 0px 0px 56vw 16vw rgba(0, 0, 0, 0.5);
}

</style>

