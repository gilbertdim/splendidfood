<template>
    <main class="wrapper">
        <h1>Past Orders</h1>

        <table class="product-table">
          <thead>
            <tr>
              <td><span class="sr-only">Product Image</span></td>
              <td>Product</td>
              <td>Price</td>
              <td>Quantity</td>
              <td>Total</td>
              <td><span class="sr-only">Actions</span></td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(checkout, i) in checkoutItems" :key="i">
              <td><i :class="'icofont-' + inventory[checkout.index].icon" class="icofont-4x" /></td>
              <td>{{ inventory[checkout.index].name }}</td>
              <td>{{ inventory[checkout.index].price.USD }}</td>
              <td>{{ checkout.quantity }}</td>
              <td>{{ itemTotal(checkout) }}</td>
              <td><button @click="addToCart(i, checkout.id, inventory[checkout.index].name, checkout.quantity)" class="btn btn-dark">Add</button></td>
            </tr>
          </tbody>
        </table>
    </main>
</template>

<script>
export default {
  props: ['checkoutItems', 'inventory', 'addToCart'],
  methods: {
    itemTotal (item) {
      return (item.quantity * this.inventory[item.index].price.USD).toFixed(2)
    }
  }
}
</script>
