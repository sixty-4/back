<template>
  <Details />
  <nav class="lg:ml-1 mb-5 mt-4 grid grid-cols-5 gap-2 text-base lg:text-xl lg:mt-5 xl:mt-10">
    <Navs />
  </nav>
  <Submit/>
</template>

<script>
import Details from './utilbar/Details.vue'
import Navs from './utilbar/Navs.vue'
import Submit from './utilbar/Submit.vue'

export default {
  name: 'UtilBar',

  components: {
    Details,
    Navs,
    Submit,
  },

  methods: {
    navToQuest (id, num) {
      this.$emit('question-changed', id, num);
    },
  },

}
</script>

