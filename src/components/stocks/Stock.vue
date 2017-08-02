<template>
    <div class="col-sm-6 col-md-4">
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">
                    {{stock.name}}
                    <small>(Price: {{stock.price}})</small>
                </h3>
            </div>

            <div class="panel-body">
                <div class="pull-left" :class="{'has-error': insufficientFunds}">
                    <input class="form-control"
                           v-model.number="quantity"
                           type="number"
                           placeholder="Quantity">
                </div>

                <div class="pull-right">
                    <button class="btn btn-success"
                            :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)"
                            @click.prevent="buyStock">
                        {{insufficientFunds ? 'Insufficient' : 'Buy' }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app-stock',
        props: ['stock'],
        methods: {
            buyStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };

                this.$store.dispatch('buyStock', order);
                this.quantity = 0;
            }
        },
        data() {
            return {
                quantity: 0
            };
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            },
            insufficientFunds() {
                return this.quantity * this.stock.price > this.funds;
            }
        }
    }
</script>