<template>
  <div id="app">
    <div class="flex-break">
      <Userdisplay />
      <Userdisplay />
      <Userdisplay />
      <Userdisplay />
    </div>
  </div>
</template>

<script>
import Userdisplay from 'src/components/Userdisplay.vue'
export default {
  name: 'App',
  components: {
    Userdisplay
  },
  data: function () {
    return {
      id: 1,
      name: 'Yatogami Tohka',
      tel: '055-555-5555',
      type: 'Saldanfon',
      location: '1202A'
    }
  }
}
</script>

<style lang="sass" scoped>
</style>
