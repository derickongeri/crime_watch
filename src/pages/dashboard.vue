<template>
  <q-page style="background-color:black;">
    <Mappanel/>
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

