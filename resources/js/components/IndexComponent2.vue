<template>

    <div class="row">
        <h1>Hello</h1>

        <table class="table">
            <thead>
            <tr>
                <th>SKU</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="sku in skus">
                <th>{{sku}}</th>
            </tr>
            </tbody>
        </table>

    </div>

</template>

<script>
  export default {
    props: [
        'skus'
    ],
    mounted () {
        console.log(this.skus)
    }
  }
</script>

<style scoped>

</style>
