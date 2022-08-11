<template>
    <v-container>
        <h1 style="font-family: Nunito, sans-serif; margin-bottom: 1%; margin-left: 1%;">CADASTRO DE PRODUTOS</h1>
        <v-form style="background-color: #f57f1f; padding: 2%; border-radius: 10px;">
            <v-row style="margin-bottom: -4%">
                <v-col
                    cols="6"
                >
                    <v-text-field
                        v-model="product.name"
                        solo
                        placeholder='Nome do produto'
                    >
                    </v-text-field>
                </v-col>
                <v-col>
                    <v-autocomplete
                        v-model="product.idCategory"
                        :items="categories"
                        clearable
                        item-text="name"
                        item-value="id"
                        solo
                        placeholder="Categoria"
                    ></v-autocomplete>
                </v-col>
                <v-col cols="3">
                    <v-text-field
                        v-model="product.price"
                        solo
                        placeholder="Preço"
                        v-mask="['#.##', '##.##', '###.##', '####.##', '#####.##']"
                        prepend-inner-icon="mdi-currency-usd"
                    >
                    </v-text-field>
                </v-col>
            </v-row>
            <v-row>
                <v-col>
                    <v-textarea
                        v-model="product.description"
                        solo
                        placeholder="Descrição"
                        rows="9"
                        style="margin-bottom: -3%;"
                    >
                    </v-textarea>
                </v-col>
            </v-row>
            <v-row>
                <v-col>
                    <v-text-field
                        v-model="product.imageLink"
                        solo
                        placeholder="Link da imagem"
                        prepend-inner-icon="mdi-image"
                        style="margin-bottom: -4%;"
                    >
                    </v-text-field>
                </v-col>
            </v-row>
            <v-row>
                <v-col>
                    <v-img
                    :src="product.imageLink"
                    style="max-width: 300px; max-height: 300px;"
                    >
                    </v-img>
                </v-col>
            </v-row>
            <v-row style="text-align: right;">
                <v-col>
                    <v-btn
                        x-small
                        solo
                        class="ma-2"
                        color="gray darken-4"
                        height="44"
                        to="/admin/products"
                    >
                    <v-icon>
                        mdi-close-box
                    </v-icon>
                    </v-btn>
                    <v-btn
                        x-small
                        solo
                        class="ma-2"
                        color="gray darken-4"
                        height="44"
                        @click="newProduct"
                    >
                        <v-icon>
                            mdi-plus-box
                        </v-icon>
                    </v-btn>
                </v-col>
            </v-row>
        </v-form>
    </v-container>
</template>

<script>
export default {
    name: 'EditProductsAdmin',
    layout: 'admin',

    data () {
        return {
            valid: false,
            product: {
                id: '',
                name: '',
                price: '',
                idCategory: '',
                description: '',
                imageLink: '',
            },
            rules: {
                required: value => !!value || 'Esse campo é obritório',
            },
            categories: []
        }
    },

    created() {
        this.getCategories()
    },

    methods: {
        async getCategories () {
            this.categories = await this.$api.get('/categories').then(resp => resp.data)
        },

        async newProduct () {
            try {
                let product = {
                    name: this.product.name,
                    price: this.product.price,
                    idCategory: this.product.idCategory,
                    description: this.product.description,
                    imageLink: this.product.imageLink
                };
                let response = await this.$api.post('/products', product)
                if(response.type !== 'success') {
                    return this.$toast.error(response.message);
                }
                this.$toast.success(response.message);
                this.$router.push("/admin/products")
            } catch (error) {
                this.$toast.error(error.message);
            }
        },
    }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Nunito');
</style>