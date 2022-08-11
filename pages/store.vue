<template>
    <v-container>
        <v-container>
          <h1 style="font-family: Nunito, sans-serif;">PRODUTOS</h1>
        </v-container>
        <hr>
        <v-row style="margin-top: 2%">
            <v-col
            v-for="n in 8"
            :key="n"
            cols="3"
            >
            <v-card height="250"></v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
  export default {
    name: 'storePage',
    layout: 'default'
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito');
</style>