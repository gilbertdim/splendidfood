<template>
    <div class="card">
        <div class="card-title">
            {{ localProduct.name }}
        </div>
        <div class="card-body">
            <i class="icofont-10x" :class="'icofont-' + localProduct.icon"></i>
            <form>
            <div class="row">
                <div class="cell">
                <label>Type:</label>
                </div>
                <div class="cell">
                <em>{{ localProduct.type }}</em>
                </div>
            </div>
            <div class="row">
                <div class="cell">
                <label>Price:</label>
                </div>
                <div class="cell">
                ${{ localProduct.price.USD }}
                </div>
            </div>
            <div class="row">
                <div class="cell">
                <label>Quantity:</label>
                </div>
                <div class="cell">
                <input type="number" v-model="quantity">
                </div>
            </div>
            </form>
        </div>
        <div class="card-footer">
            <button @click="quantity = addToCart(index, localProduct.id, localProduct.name, quantity)" class="btn btn-light">
            Add to cart
            </button>
        </div>
    </div>
</template>

<script>
export default {
  props: ['product', 'inventory', 'index', 'addToCart'],
  data () {
    return {
      localProduct: this.product,
      localInventory: this.inventory,
      quantity: 0
    }
  }
}
</script>
