<template>
  <main class="container">
    <section class="image" :style="`background:url(/${currentItem.img}) no-repeat center center`"></section>
    <section class="details">
      <h2>{{ currentItem.item }}</h2>
      <h3>Price: {{ currentItem.price.toFixed(2) }}</h3>
      <input type="number" /><button>Add to cart</button>
    </section>
    <section v-if="currentItem.options"  class="options">
      <fieldset>
        <legend>
          <h3>Options</h3>
        </legend>
        <div v-for="option in currentItem.options" type="radio" :key="option">
          <label>{{ option }}</label>
          <input type="radio" name="option" :id="option" :value="option" v-model="itemOptions"/>
        </div>
      </fieldset>
    </section>
    <section class="addons">
      <fieldset>
        <legend>
          <h3>Add ons</h3>
        </legend>
        <div v-for="addOn in currentItem.addOns" type="radio" :key="addOn">
          <label>{{ addOn }}</label>
          <input type="radio" name="addOn" :id="addOn" :value="addOn" v-model="itemAddOns"/>
        </div>
      </fieldset>
    </section>
  </main>
</template>

<script>
import { mapState } from "vuex";

export default {
  data() {
    return {
      id: this.$route.params.id,
      itemOptions: null,
      itemAddOns: null
    };
  },
  computed: {
    ...mapState(["fooddata"]),
    currentItem() {
      // more efficient than forEach because we can break
      let result;

      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          if (this.fooddata[i].menu[j].id === this.id) {
            result = this.fooddata[i].menu[j];
            break;
          }
        }
      }
      console.log(result, this.foodata)

      return result;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 1000px;
  margin: 100px auto;
  display: grid;
  grid-template-columns: 400px 1fr;
  grid-template-rows: 400px 1fr;
  grid-column-gap: 60px;
  grid-row-gap: 60px;
  line-height: 2;
}

.image {
  grid-area: 1 / 1 / 2 / 2;
  background-size: cover;
}
.details {
  grid-area: 1 / 2 / 2 / 3;
  position: relative;
}
.options {
  grid-area: 2 / 1 / 3 / 2;
}
</style>
