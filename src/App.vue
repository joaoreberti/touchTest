<template>
    <v-app>
        <p class="text-h1">joao</p>
        <v-main>
            <router-view></router-view>
        </v-main>
    </v-app>
</template>

<style lang="scss" scoped>

    .text-h1{
    color: $joao;

    }

</style>
<script>
export default {
    name: "App",
    data: () => ({
        //
    }),
};
</script>
