<template>
    <div class="list-stocks">
        <template v-for="stock in stocks">
            <app-stock :stock="stock"></app-stock>
        </template>
    </div>
</template>

<script>
    import AppStock from "./Stock.vue";

    export default {
        components: {AppStock},
        name: 'app-stocks',
        computed: {
            stocks() {
                return this.$store.getters.stocks;
            }
        }
    }
</script>

