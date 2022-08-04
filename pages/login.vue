<template>
    <v-container style="background-color: red;">
        <v-row>
            <v-col style="background-color: green">
                <h1 style="font-size: xx-large;">
                    FAÇA O LOGIN NA PLATAFORMA
                </h1>
            </v-col>
            <v-col style="background-color: blue">
                <v-text-field
                    solo
                    placeholder="Username"
                >
                </v-text-field>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
    name: 'LoginPage',
    layout: 'login'
}
</script>

<style>
</style>