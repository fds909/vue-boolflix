<template>
  <main>
    <ul v-for="(elem, index) in movies" :key="index">
        <li>{{ elem.title }}</li>
        <li>{{ elem.originalTitle }}</li>
        <li>{{ elem.language }}</li>
        <li>{{ elem.vote }}</li>
    </ul>
  </main>
</template>

<script>
export default {
  name: 'MainComp',
  props: ['movies'],
  data() {
      return {
          
      }
  }
}
</script>

<style scoped lang="scss">

</style>
