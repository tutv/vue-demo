<template>
    <div class="col-sm-6 col-md-4">
        <div class="panel panel-info">
            <div class="panel-heading">
                <h3 class="panel-title">
                    {{stock.name}}
                    <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
                </h3>
            </div>

            <div class="panel-body">
                <div class="pull-left" :class="{'has-error': insufficientQuantity}">
                    <input class="form-control"
                           v-model.number="quantity"
                           type="number"
                           placeholder="Quantity">
                </div>

                <div class="pull-right">
                    <button class="btn btn-success"
                            :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(quantity)"
                            @click.prevent="sellStock">
                        {{insufficientQuantity ? 'Not enough' : 'Sell'}}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import {mapActions} from 'vuex';

    export default {
        name: 'app-stock-portfolio',
        props: ['stock'],
        methods: {
            ...mapActions({
                'placeSellOrder': 'sellStock'
            }),
            sellStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };

                this.placeSellOrder(order);
                this.quantity = 0;
            }
        },
        data() {
            return {
                quantity: 0
            };
        },
        computed: {
            insufficientQuantity() {
                return this.quantity > this.stock.quantity
            }
        }
    }
</script>
