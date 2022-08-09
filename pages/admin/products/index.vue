<template>
    <v-container>
        <h1 style="font-family: Nunito, sans-serif; margin-left: 1%;">CONSULTA DE PRODUTOS</h1>
        <v-container>
            <v-row>
                <v-col>
                    <v-btn color="orange darken-2">
                        Procurar
                    </v-btn>
                    <v-btn
                        color="orange darken-2"
                        to="/admin/products/new"
                    >
                        Novo produto
                    </v-btn>
                </v-col>
            </v-row>
        </v-container>
        <v-container>
            <v-data-table
                :headers="headers"
                :items-per-page="10"
            >
                <template v-slot:item.actions="{ item }">
                    <v-icon
                        small
                        class="mr-2"
                        @click="editar(item)"
                    >
                        mdi-pencil
                    </v-icon>
                    <v-icon
                        small
                        @click="deletar(item)"
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
    name: 'AdminConsultaProdutos',
    layout: 'admin',

    data () {
        return {
            headers: [
                {
                    text: 'Código',
                    align: 'center',
                    sortable: false
                },
                {
                    text: 'Nome',
                    align: 'center',
                    sortable: false
                },
                {
                    text: 'Categoria',
                    align: 'center',
                    sortable: false
                }
            ]
        }
    }
}
</script>

<style>
</style>