<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
        <router-link to="/" class="top-bar-link">
          <i class="icofont-spoon-and-fork"></i>
          <span>Home</span>
        </router-link>
        <router-link to="/products" class="top-bar-link">
          <span>Products</span>
        </router-link>
        <router-link to="/past-orders" class="top-bar-link">
          <span>Past Orders</span>
        </router-link>
    </nav>

    <div href="#" @click="toggleSidebar" class="top-bar-cart-link">
        <i class="icofont-cart-alt icofont-1x"></i>
        <span>Cart ({{ totalQuantity }})</span>
    </div>

  </header>

  <router-view @click="showSidebar=false" :inventory="inventory" :checkoutItems="checkoutItems" :addToCart="addToCart" />

  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
    :clearCart="clearCart"
    :checkoutItems="checkoutItems"
  />

</template>

<script>
import Sidebar from '@/components/Sidebar.vue'
import food from '@/food.json'

export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {},
      checkoutItems: (window.localStorage.checkout !== undefined ? JSON.parse(window.localStorage.checkout) : [])
    }
  },
  computed: {
    totalQuantity () {
      const total = Object.values(this.cart).reduce((acc, item, index) => {
        return acc + item.quantity
      }, 0)

      return total
    }
  },
  methods: {
    addToCart (i, id, name, quantity) {
      if (quantity > 0) {
        if (!this.cart[name]) {
          this.cart[name] = {
            index: i,
            id: id,
            quantity: 0
          }
        }

        this.cart[name].quantity += quantity
      }

      return 0
    },
    clearCart () {
      this.cart = {}
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (index) {
      var item = this.cart[index]

      item.quantity -= 1
      if (item.quantity === 0) {
        delete this.cart[index]
      }
    }
  }
}
</script>

<style>
  body {
    margin: 0px
  }
</style>
