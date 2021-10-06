<script>
export default {
  name: "MenuItem",
  props: ["addToShoppingCart", "image", "inStock", "name", "price", "quantity"],
  computed: {
    generatedPrice() {
      if (this.onSale) {
        return (this.price * 0.9).toFixed(2);
      } else {
        return this.price;
      }
    },
  },
  beforeMount() {
    const todayDay = new Date().toJSON().slice(8, 10);
    if (todayDay % 2 === 0) this.onSale = true;
  },
};
</script>

<template>
  <div class="menu-item">
    <img class="menu-item__image" :src="image.source" :alt="image.alt" />
    <div>
      <h3>{{ name }}</h3>
      <p>Prix : {{ generatedPrice }}</p>
      <p v-if="inStock">En stock</p>
      <p v-else>En rupture de stock</p>
      <div class="adding-menu">
        <label for="add-item-quantity">Quantité : {{ quantity }}</label>
        <input v-model.number="quantity" id="add-item-quantity" type="number" />
        <button @click="addToShoppingCart(quantity)">Ajouter au panier</button>
      </div>
    </div>
  </div>
</template>

<style>
img {
  width: 300px;
  margin: 20px;
}

.menu-item {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.adding-menu {
  display: flex;
  flex-direction: column;
  width: 100px;
}
.adding-menu > * {
  margin: 5px;
}
</style>