<template>
  <v-app dark>
    <v-navigation-drawer v-model="drawer" :mini-variant="miniVariant" :clipped="clipped" floating expand-on-hover app
      src="https://img.elo7.com.br/product/zoom/37C1703/papel-de-parede-adesivo-hamburgueria-preto.jpg"
      style="border-radius: 14px; margin-left: 8px; margin-top: 8px; height: 90%;"
      >
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" router exact
          style="color: white; font-family: Nunito, sans-serif; font-weight: bold">
          <v-list-item-action>
            <v-icon style="color: #f57f1f;">{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" style="color: #f57f1f;" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-icon large style="margin: 5px; margin-top: -3px; color: #f57f1f;">
        mdi-food
      </v-icon>
      <v-toolbar-title v-text="title"
        style="font-family: Nunito, sans-serif; font-size: 40px; margin-bottom: 6px; margin-left: -1px" />
      <v-spacer />
      <v-btn class="ma-2" color="orange darken-2" to="/registro">
        CADASTRAR
      </v-btn>
      <v-btn class="ma-2" color="orange darken-2" to="/login">
        ENTRAR
      </v-btn>
      <v-btn class="ma-2" to="/admin">admin</v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      clipped: true,
      drawer: true,
      items: [
        {
          icon: 'mdi-view-dashboard',
          title: 'Bem vindo!',
          to: '/'
        },
        {
          icon: 'mdi-hamburger',
          title: 'Produtos',
          to: '/store'
        },
        {
          icon: 'mdi-information',
          title: 'Sobre nós',
          to: '/história'
        }
      ],
      miniVariant: true,
      right: true,
      rightDrawer: false,
      title: 'crstore'
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito');
</style>