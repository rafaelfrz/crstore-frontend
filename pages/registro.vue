<template>
    <v-container v-model="valid" style="margin: auto; margin-top: 10%;">
        <v-row justify="center" align="center">
            <v-container style="text-align: center;">
                <v-icon x-large style="margin-top: -20px; color: #f57f1f;">
                    mdi-food
                </v-icon>
                <v-text style="font-size: 48px; font-family: 'Nunito', sans-serif;">
                    crstore
                </v-text>
            </v-container>
            <v-col style="background-color: #272727; border-radius: 10px;">
                <v-container id="registro">
                    <v-container style="padding:10%">
                        <v-row>
                            <v-text-field v-model="email" solo placeholder="Email" prepend-inner-icon="mdi-at"
                                style="margin-bottom: -18px" />
                        </v-row>
                        <v-row>
                            <v-text-field v-model="username" solo placeholder="Username"
                                prepend-inner-icon="mdi-account" style="margin-bottom: -18px" />
                        </v-row>
                        <v-row>
                            <v-text-field v-model="password" solo placeholder="Senha" prepend-inner-icon="mdi-lock"
                                style="margin-bottom:-15px" />
                        </v-row>
                        <v-row>
                            <a href="#" style="text-decoration:none; color:#f57f1f; font-weight: bold;">Esqueci a
                                senha</a>
                        </v-row>
                        <v-row style="margin-top: 24px">
                            <v-btn color="yellow darken-4" large block>
                                ENTRAR
                            </v-btn>
                            <v-row style="text-align: center">
                                <v-col style="text-align: center">
                                    <p style="margin-top: 20px"> Não tem uma conta? <a href="#"
                                            style="color: #f57f1f; text-decoration:none; font-weight: bold;">Registre-se</a>
                                    </p>
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
    name: 'CadastroPage',
    layout: 'login',
}
</script>

<style>
</style>