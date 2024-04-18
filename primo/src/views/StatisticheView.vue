<template>
  <v-container>
<h1>Statistiche</h1>
  </v-container>
</template>
<script>
export default {
  name: 'StatisticheView',
  data() {
    return {
      winner:[],
    }
  },
  methods: {
    getWinner(){
      this.winner= localStorage.getItem('winner');
    }
  },
  mounted() {
    //
  },
  created() {
    //
  },
}
</script>
