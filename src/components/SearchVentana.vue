<template>
  <div>
    <v-container>
      <div class="columns is-centered is-multiline">
        <div class="card column is-one-quarter" v-for="product in products" :key="product.id">
          <SptProducts :product="product"></SptProducts>
        </div>
        <div class="section" v-if="products.length === 0">
          <p>{{ noProductLabel }}</p>
        </div>
      </div>
    </v-container>
  </div>
</template>

<script>
import SptProducts from '../Products';
import { getByTitle } from '@/assets/filters';

export default {
  name: 'productsList',
  
  components: { SptProducts },
  
  data () {
    return {
      id: '',
      noProductLabel: 'No product found',
      productsFiltered: []
    };
  },

  computed: {
    products () {
      if (this.$store.state.userInfo.hasSearched) {
        return this.getProductByTitle();
      } else {
        return this.$store.state.products;
      }
    }
  },

  methods: {
    getProductByTitle () {
      let listOfProducts = this.$store.state.products,
          titleSearched = this.$store.state.userInfo.productTitleSearched;
      
      return this.productsFiltered = getByTitle(listOfProducts, titleSearched);
    }
  }

};
</script>




