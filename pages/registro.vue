<template>
    <v-container 
        v-model="valid"
        style="margin: auto; margin-top: 1%;"
    >
        <v-row 
            justify="center"
            align="center"
        >
            <v-container style="text-align: center;">
                <p
                    style="font-size: 48px;
                    font-family: Nunito, sans-serif;"
                >
                    <v-icon
                        x-large
                        style="margin-top: -6px; margin-right: -10px;color: #f57f1f;"
                    >
                        mdi-food
                    </v-icon>
                    crstore
                </p>
            </v-container>
            <v-col
                style="background-color: #272727; border-radius: 10px; margin-left: 20%; margin-right: 20%;"
            >
                <v-container id="registro">
                    <v-container
                        style="padding:10%;"
                    >
                        <v-row>
                            <v-text-field
                                v-model="user.email"
                                solo
                                placeholder="Email"
                                prepend-inner-icon="mdi-at"
                                style="margin-bottom: -2px;"
                                shaped
                                :rules="[rules.required, rules.email]"
                            /> 
                        </v-row>
                        <v-row>
                            <v-text-field
                                v-model="user.username"
                                solo
                                placeholder="Username"
                                prepend-inner-icon="mdi-account"
                                style="margin-bottom: -2px"
                                :rules="[rules.required, rules.username]"
                            />
                            <v-tooltip right>
                                <template v-slot:activator="{ on, attrs }">
                                    <p
                                        style="color: red; position: absolute; right: 29%; top: 296px;"
                                        v-bind="attrs"
                                        v-on="on"
                                    >
                                    *
                                    </p>
                                </template>
                                <span>Necessário: <br>- Acima de 8 caracteres</span>
                            </v-tooltip>
                        </v-row>
                        <v-row>
                            <v-text-field
                                v-model="user.password"
                                :rules="[rules.password]"
                                solo
                                placeholder="Senha"
                                prepend-inner-icon="mdi-lock"
                                style="margin-bottom:-2px;"
                                type="password"
                            />
                            <v-tooltip right>
                                <template v-slot:activator="{ on, attrs }">
                                    <p
                                        style="color: red; position: absolute; right: 29%; top: 47%"
                                        v-bind="attrs"
                                        v-on="on"
                                    >
                                    *
                                    </p>
                                </template>
                                <span>Necessário:
                                    <br>- Acima de 8 caracteres 
                                    <br>- Número 
                                    <br>- Caracter especial (@#$%) 
                                </span>
                            </v-tooltip>
                        </v-row>
                        <v-row>
                            <v-text-field
                                v-model="user.passwordMatch"
                                :rules="[rules.passwordMatch]"
                                solo
                                placeholder="Repita a senha"
                                prepend-inner-icon="mdi-lock"
                                type="password"
                                style="margin-bottom:-15    px;
                                border-bottom-left-radius: 14px;
                                border-bottom-right-radius: 14px;"
                            />
                        </v-row>
                        <v-row style="margin-top: 24px">
                            <v-btn
                                color="yellow darken-4"
                                large
                                block
                                @click="register"
                            >
                                REGISTRAR-SE
                            </v-btn>
                            <v-container
                                class="px-0"
                                fluid
                                style="margin-bottom: -6%;"
                            >
                                <v-checkbox
                                    v-model="checkbox"
                                    label="Aceita os termos de uso?"
                                >
                                </v-checkbox>
                            </v-container>
                            <v-row style="text-align: center">
                                <v-col style="text-align: center">
                                    <p style="margin-top: 20px">
                                        Já possui conta?
                                        <a href="./login"
                                            style="color: #f57f1f;
                                            text-decoration:none;
                                            font-weight: bold;">
                                            Faça login
                                        </a>
                                    </p>
                                </v-col>
                            </v-row>
                        </v-row>
                        <v-row>
                            <v-col>
                                <hr style="color: white;">
                            </v-col>
                        </v-row>
                        <v-row 
                            style="text-align: right;
                            margin-bottom: -15%"
                        >
                            <v-col>
                                <a href="./index">
                                    <v-icon style="color: #f57f1f;">mdi-close-box</v-icon>
                                </a>
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
    name: 'RegisterPage',
    layout: 'login',

    data () {
        return {
            user: {
                email: '',
                username: '',
                password: '',
                passwordMatch: '',
            },
            rules: {
                required: value => !!value || 'Esse campo é obrigatório',
                email: value => {
                    const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
                    return pattern.test(value) || 'O e-mail não é válido'
                },
                username: value => {
                    const pattern = /^[A-Za-z][A-Za-z0-9_]{7,29}$/
                    return pattern.test(value) || 'O nome de usuário não é válido'
                },
                password: value => {
                    const pattern = /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$/
                    return pattern.test(value) || 'Senha fora dos paramêtros'
                },
                passwordMatch: value => value === this.user.password || 'As senhas devem ser iguais'
            },
        }
    },

    methods: {
        async register () {
            try {
            let user = {
                email: this.user.email,
                password: this.user.password,
                username: this.user.username,
            };
            let response = await this.$api.post('/users/register', user);
            console.log(response)
            if (response.type !== 'success') {
                return this.$toast.error(response.message);
            }
            this.$toast.success(response.message)
            this.$router.push('/');
            } catch (error) {
                this.$toast.error(response.message)
            }
        },

        async emailInUse () {
            
        }
    }
}
</script>

<style>
</style>