<template>
    <div class="portfolio">
        <template v-for="stock in stocks">
            <app-stock-portfolio :stock="stock"></app-stock-portfolio>
        </template>
    </div>
</template>

<script>
    import {mapGetters} from 'vuex';
    import AppStockPortfolio from "./Stock.vue";

    export default {
        components: {AppStockPortfolio},
        name: 'app-portfolio',
        computed: {
            ...mapGetters({
                stocks: 'stockPortfolio'
            })
        }
    }
</script>