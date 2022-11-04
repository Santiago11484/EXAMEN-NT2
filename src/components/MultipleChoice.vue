<template>
  <section class="src-components-multiplechoice">
      <div class="jumbotron">
        <h2>Multiple Choice</h2>
        <hr>
        <hr>
        <br>

        <table class="table responsive table-dark">
        <tr>
          <th>Número de Pregunta</th>
          <th>Respuesta</th>        
        </tr>
        <tr v-for="(respuesta,index) in respuestas" :key="index">
          <th> {{respuesta.numero}} </th>
          <th> {{respuesta.resp}} </th>          
        </tr>
      </table>
      </div>
  </section>
</template>

<script>

  export default  {
    name: 'src-components-multiple-choice',
    props: [],
    mounted () {

    },
    data () {
      return {
        respuestas: [
          {numero: 1, resp: 'B y D'},
          {numero: 2, resp: 'C'},
          {numero: 3, resp: 'B y E'}
        ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-multiple-choice {

  }
</style>
