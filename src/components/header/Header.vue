<template>
  <div class="font-['Trebuchet MS']">
    <h2 class="p-2 lg:p-3 font-bold text-xl sm:text-2xl tracking-tight">
      <b class="text-brown4">C</b>
      <b class="text-red-400">B</b>
      Easy
    </h2>
  </div>
  <Menu />
</template>

<script>
import Menu from './menu/Menu.vue'
import { useDataStore } from '../../store/data.js'

export default {
  name: 'Header',

  setup() {
    const dataStore = useDataStore()

    return {
      dataStore,
    }
  },
  
  components: {
    Menu,
  },
}
</script>
