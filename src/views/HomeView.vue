<template>
  <div class="home container">
    <h1 class="my-4">LISTA DE CURSOS</h1>
    <div class="cursos">
      <CursoCard v-for="curso in cursos" :curso="curso" :key="curso.id"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import CursoCard from '@/components/CursoCard.vue';
import { mapState } from 'vuex';

export default {
  name: 'HomeView',
  components: {
    CursoCard,
  },
  computed: {
    ...mapState({
      cursos: (state)=>state.cursos
    })
  },
}
</script>

<style scoped>
  .cursos{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
</style>