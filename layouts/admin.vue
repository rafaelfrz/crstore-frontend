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
      <v-spacer/>
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
          icon: 'mdi-account-circle',
          title: 'Clientes',
          to: '/admin/customer'
        },
        {
          icon: 'mdi-hamburger',
          title: 'Produtos',
          to: '/admin/products'
        },
        {
          icon: 'mdi-package-variant-closed',
          title: 'Pedidos',
          to: '/admin/orders'
        },
        {
          icon: 'mdi-format-list-group',
          title: 'Categorias',
          to: '/admin/categories'
        },
        {
          icon: 'mdi-sale',
          title: 'Descontos',
          to: '/admin/discounts'
        },
      ],
      miniVariant: true,
      right: true,
      rightDrawer: false,
      title: 'crstore'
    }
  },

  // async created () {
  //   await this.validateLogin();
  // },

  // methods: {
  //   async validateLogin () {
  //     const token = localStorage.getItem('crstore-api-token') || '';
  //     let response = await this.$axios.$get('http://localhost:3333/users/validate-token', {
  //       headers: { Authorization: `Bearer ${token}` }
  //     });
  //     if (response.type !== 'success' || response.data?.role !== 'admin') {
  //       this.$toast.info('Você não tem permissão para acessar esse recurso');
  //       return this.$router.push({ name: 'index' });
  //     } 
  //   }
  // }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito');
</style>