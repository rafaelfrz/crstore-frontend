<template>
    <v-container>
        <h1 style="font-family: Nunito, sans-serif; margin-left: 1%;">CONSULTA DE CATEGORIAS</h1>
        <v-container>
            <v-row>
                <v-col>
                    <v-btn color="orange darken-2">
                        Procurar
                    </v-btn>
                    <v-btn
                        color="orange darken-2"
                        @click="toggleCadastro"
                    >
                        Nova categoria
                    </v-btn>
                </v-col>
            </v-row>
        </v-container>
        <v-expand-transition>
            <v-container v-if="cadastro" style="margin-bottom: -24px;">
                <v-row>
                    <v-col cols="11">
                        <v-text-field
                            v-model="category.name"
                            solo
                            placeholder="Nome nova categoria"
                        >
                        </v-text-field>
                    </v-col>
                    <v-col>
                        <v-btn
                            x-small
                            height="48"
                            width="48"
                            color="orange darken-2"
                            style="font-size: x-large; float:right"
                            @click="newCategory"
                            >
                            +
                        </v-btn>
                    </v-col>
                </v-row>
            </v-container>
        </v-expand-transition>
        <v-container>
            <v-data-table
                :headers="headers"
                :items="categories.data"
                :items-per-page="10"
                class="elevation-1"
            >
                <template v-slot:item.actions="{ item }">
                    <v-icon
                        small
                        @click="destroy(item)"
                    >
                        mdi-delete
                    </v-icon>
                </template>
            </v-data-table>
        </v-container>
    </v-container>
</template>

<script>
export default {
    name: 'AdminConsultaCategorias',
    layout: 'admin',

    data () {
        return {
            category: {
                name: ''
            },
            cadastro: false,
            headers: [
                {
                    text: 'Código',
                    align: 'center',
                    sortable: false,
                    value: 'id'
                },
                {
                    text: 'Nome',
                    align: 'center',
                    sortable: false,
                    value: 'name'
                },
                {
                    text: 'Qtd. produtos',
                    align: 'center',
                    sortable: false
                },
                { text: "", value: "actions" }
            ],
            categories: []
        }
    },

    created () {
        this.getCategories();
    },

    methods: {
        toggleCadastro () {
            this.cadastro = !this.cadastro
        },

        async getCategories () {
            this.categories = await this.$api.get('/categories')
        },

        async newCategory () {
            try {
                let category = {
                    name: this.category.name
                };
                let response = await this.$api.post('/categories', category);
                if (response.type !== 'success') {
                    return this.$toast.error(response.message)
                }
                this.$toast.success(response.message);
                this.getCategories ();
                this.toggleCadastro();
            } catch (error) {
                this.$toast.error(error.message);
            }
        },

        async destroy(category) {
            try {
                if(confirm('Deseja deletar a categoria?')) {
                    let response = await this.$api.post('/categories/destroy', {id: category.id})
                    this.$toast.success(response.message);
                    this.getCategories();
                }
            } catch (error) {
                this.$toast.error(response.message)
            }
        }

    }
}
</script>

<style>
</style>
