<template>
  <section class="items">
      <div v-for="product,index of products" class="product" :class="{ 'selected':product.active }"
          @click="product.active = !product.active" :key="index">
          <div class="photo">
            <img :src="'/img/'+product.photo">
          </div>
          <div class="description">
              <span class="name">{{ product.name }}</span>
              <span class="price">$ {{ product.price }}</span>
              <div class="quantity-area" v-if="product.active">
                  <button @click.stop="product.quantity--" :disabled="product.quantity <= 1">-</button>
                  <span class="quantity">{{ product.quantity }}</span>
                  <button @click.stop="product.quantity++">+</button>
              </div>
          </div>
      </div>
  </section>
  <section class="summary" v-if="total()>0">
    <strong>Order Details</strong>
    <table>
        <thead>
            <tr>
                <th>Item</th>
                <th>Total</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product,index in products" :key="index">
                <template v-if="product.active">
                  <td>{{ product.quantity + ' x ' + product.name}}</td>
                  <td>{{ (product.quantity * product.price).toFixed(2) }}</td>
                </template>
            </tr>
            <tr>
                <th>Total</th>
                <th>{{ total() }}</th>
            </tr>
        </tbody>
    </table>
  </section>
</template>

<script>
export default {
  name: 'App',
  data(){
    return { products : [
    {
        "photo": "big-mac.png",
        "name": "Big Mac",
        "price": 5.99,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "mc-chicken.png",
        "name": "Mc Chicken",
        "price": 4.99,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "double-cb.png",
        "name": "Double Cheese Burger",
        "price": 2.99,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "fries.png",
        "name": "Fries",
        "price": 2.99,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "nuggets.png",
        "name": "Mc Nuggets",
        "price": 3.49,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "salad.png",
        "name": "Salad",
        "price": 2.79,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "cola.png",
        "name": "Coke",
        "price": 1.99,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "lipton.png",
        "name": "Ice Tea",
        "price": 1.99,
        "active": false,
        "quantity": 1
    },
    {
        "photo": "water.png",
        "name": "Water",
        "price": 1.49,
        "active": false,
        "quantity": 1
    }]
  };},
  components: {
  },
  methods: {
    total: function () {
        var total = 0;
        this.products.forEach(function (product) {
            if (product.active) {
                total += product.price * product.quantity;
            }
        });
        return total.toFixed(2);
    }
  }
}
</script>
 
<style scoped lang="css">
</style>