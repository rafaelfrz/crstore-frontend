<template>
  <v-container v-model="valid" style="margin: auto; margin-top: 13%;">
    <v-row justify="center" align="center">
      <v-col cols="6">
        <v-container style="text-align: center;">
          <v-icon x-large style="margin-top: -20px; color: #f57f1f;">
            mdi-food
          </v-icon>
          <v-text style="font-size: 48px; font-family: 'Nunito', sans-serif;">
            crstore
          </v-text>
        </v-container>
        <v-container style="margin-right: -6%; margin-top: -6%">
          <v-text style="font-size: 72px; font-family: 'Nunito', sans-serif; font-weight: thin;">
            Faça seu login na plataforma
          </v-text>
        </v-container>
      </v-col>
      <v-col cols="6" style="background-color: #272727; border-radius: 10px;">
        <v-container id="login">
          <v-container style="padding:10%">
            <v-row>
              <v-text-field v-model="email" solo placeholder="Email" prepend-inner-icon="mdi-at"
                style="margin-bottom: -18px" />
            </v-row>
            <v-row>
              <v-text-field v-model="password" solo placeholder="Senha" prepend-inner-icon="mdi-lock"
                style="margin-bottom:-15px" />
            </v-row>
            <v-row>
              <a href="#" style="text-decoration:none; color:#f57f1f; font-weight: bold;">Esqueci a senha</a>
            </v-row>
            <v-row style="margin-top: 24px">
              <v-btn color="yellow darken-4" large block>
                ENTRAR
              </v-btn>
              <v-row style="text-align: center">
                <v-col style="text-align: center">
                  <p style="margin-top: 20px"> Não tem uma conta? <a href="#"
                      style="color: #f57f1f; text-decoration:none; font-weight: bold;">Registre-se</a> </p>
                </v-col>
              </v-row>
            </v-row>
            <v-row>
              <v-col>
                <hr style="color: white;">
              </v-col>
            </v-row>
          </v-container>
        </v-container>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  name: 'LoginPage',
  layout: 'login',

  data() {
    return {
      valid: false,
      showPassword: false,
      email: '',
      password: '',
      rules: {
        required: value => !!value || 'Esse campo é obrigatório',
        email: value => {
          const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
          return pattern.test(value) || 'O e-mail não é válido'
        }
      },

      methods: {
        async login() {
          if (!this.valid) {
            return this.$toast.info('Teste')
          }
          let user = {
            email: this.email,
            password: this.password
          };
          let response = await this.$api.post('/user/login', user);
          if (response.type !== 'success') {
            return this.$toast.error(response.message);
          }
          this.$toast.success(response.message)
          localStorage.setItem('crstore-api-token', response.token)
        },

        toggleShowPassword() {
          this.showPassword = !this.showPassword
        },
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito');
</style>