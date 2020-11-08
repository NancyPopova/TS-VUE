<template>
    <div>
        <form >
            <div class="filters row">
                <!--            <div class="col-sm-6 col-md-3">-->
                <!--                <label for="price_from">@lang('main.price_from')-->
                <!--                    <input type="text" name="price_from" id="price_from" size="6" value="{{ request()->price_from}}">-->
                <!--                </label>-->
                <!--                <label for="price_to">@lang('main.to')-->
                <!--                    <input type="text" name="price_to" id="price_to" size="6"  value="{{ request()->price_to }}">-->
                <!--                </label>-->
                <!--            </div>-->

                <div class="col-sm-2 col-md-2">
                    <input type="checkbox" id="new" value="new" v-model="checkedFilters">
                    <label> Новинка </label>
                </div>
                <div class="col-sm-2 col-md-2">
                    <input type="checkbox" id="hit" value="hit"  v-model="checkedFilters">
                    <label> Хит </label>
                </div>
                <div class="col-sm-2 col-md-2">
                    <input type="checkbox" id="recommend" value="recommend" v-model="checkedFilters">
                    <label> Рекомендуем </label>
                </div>

            </div>
        </form>

        <div class="row">
            <div class="col-sm-6 col-md-4" v-for="product in filteredProducts">
                <div class="labels">
                    <span v-if="product.new == 1" class='badge badge-success'>Новинка</span>

                    <span v-if="product.hit == 1" class='badge badge-warning'>Хит</span>

                    <span v-if="product.recommend == 1" class='badge badge-danger'>Рекомендуем</span>
                </div>
                <div class="thumbnail">
                    <img :src="`/images/${product.image}`" :alt="product.name" >
                    <div class="caption">
                        <h3>{{ product.name }}</h3>

                        <button type="submit" class="btn btn-primary" role="button">Добавить в корзину</button>

                        <a href="{{}}"
                           class="btn btn-default" role="button">Подробнее</a>

                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>

export default {
    name: "index",
    props: [
        'products',

    ],
    data () {
        return {
            checkedFilters:[],
            sortedProducts:[]
        }
    },
    mounted() {
        console.log(this.products);
    },

    computed: {
        filteredProducts ()
        {
            if (this.sortedProducts.length) {
                return this.sortedProducts
            } else {
                return this.products
            }
        },
    },

    watch: {
            checkedFilters : function () {
                this.sortBy();
            }
    },


    methods: {

        sortBy() {
            this.sortedProducts = [];
            let vm = this;


            if (this.checkedFilters.includes('hit')) {
                this.products.map(function (item) {
                    if (item.hit == 1) {
                        vm.sortedProducts.push(item);
                    }
                })
            }
            if (this.checkedFilters.includes('new')){
                this.products.map(function (item) {
                    if (item.new == 1) {
                        vm.sortedProducts.push(item);
                    }
                })
            }
            if (this.checkedFilters.includes('recommend')) {
                this.products.map(function (item) {
                    if (item.recommend == 1) {
                        vm.sortedProducts.push(item);
                    }
                })
            }

        },
    }
}
</script>

<style scoped>

</style>

