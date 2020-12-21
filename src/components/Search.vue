<template>
  <v-toolbar color="orange accent-1">
    <v-btn icon> <v-icon>mdi-arrow-left</v-icon> </v-btn>
    <v-toolbar-title class="title mr-6 hidden-sm-and-down">
      Search
    </v-toolbar-title>
    <v-autocomplete
      v-model="model"
      :items="items"
      :loading="isLoading"
      :search-input.sync="search"
      chips
      clearable
      hide-details
      hide-selected
      item-text="name"
      item-value="symbol"
      label="Search"
      solo
    >
      <template v-slot:no-data>
        <v-list-item>
          <v-list-item-title>
            Search for your favorite
            <strong>Products</strong>
          </v-list-item-title>
        </v-list-item>
      </template>
      <template v-slot:selection="{ attr, on, item, selected }">
        <v-chip
          v-bind="attr"
          :input-value="selected"
          color="blue-grey"
          class="white--text"
          v-on="on"
        >
          <v-icon left>
            mdi-bitcoin
          </v-icon>
          <span v-text="item.name"></span>
        </v-chip>
      </template>
      <template v-slot:item="{ item }">
        
          <v-chip v-for="(keyword, i) in keywords" :key="i"  class="mr-2"   >
            {{ keyword }}
          </v-chip>
        
       
        <v-img
          :src="item.src"
          class="mr-4"
          max-width="64"
          min-width="64"
        ></v-img>
        <v-list-item-content>
          <span
            class="text-uppercase font-weight-regular caption"
            v-text="item.type"
          ></span>
          <v-list-item-title v-text="item.name"></v-list-item-title>
          <v-list-item-subtitle v-text="item.symbol"></v-list-item-subtitle>
        </v-list-item-content>
        <v-list-item-action>
          <v-icon>mdi-bitcoin</v-icon>
        </v-list-item-action>       
        
      </template>
    </v-autocomplete>
    <template v-slot:extension>
      <v-tabs
        v-model="tab"
        :hide-slider="!model"
        color="blue-grey"
        slider-color="blue-grey"
      >
        <v-tab :disabled="!model">
          News
        </v-tab>
        <v-tab :disabled="!model">
          Trading
        </v-tab>
        <v-tab :disabled="!model">
          Blog
        </v-tab>
      </v-tabs>
    </template>
  </v-toolbar>

  
 
</template>

<script>
  export default {
    data: () => ({
      isLoading: false,
      items: [
        {
          id:1,
          name:'Gafas',
          type:'Natación',
          price:'18.00',
          keyword: 'Articulos',
          src:require('../assets/img/shop/1.jpg')
        },
        {
          id:2,
          name:'Balón Mikasa ',
          type:'Voleibol',
          price:'40.00',
          keyword: 'Articulos',
          src:require('../assets/img/shop/2.jpg')
        
        },
        {
          id:3,
          name:'Zara limited...',
          type:'Denim',
          price:'25.00',
          keyword: 'Ropa',
          src:require('../assets/img/shop/3.jpg')
        },
        {
          id:4,
          name:'Balon Adidas',
          type:'Futbol',
          price:'30.00',
          keyword: 'Articulo',
          src:require('../assets/img/shop/4.jpg')
        },
        {
          id:5,
          name:'Zapatos',
          type:'Atletismo',
          price:'50.00',
          keyword: 'Calzado',
          src:require('../assets/img/shop/5.jpg')
        },
        {
          id:6,
          name:'Raquetas',
          type:'Tenis',
          price:'34.00',
          src:require('../assets/img/shop/6.jpg'),
          keyword: 'Articulos',
        },
        {
          id:7,
          name:'Balón',
          type:'Baloncesto',
          price:'38.00',
          src:require('../assets/img/shop/7.jpg'),
          keyword: 'Articulos',
        },
        {
          id:8,
          name:'Rodilleras',
          type:'Implementos deportivos',
          price:'25.00',
          src:require('../assets/img/shop/8.jpg'),
          keyword: 'Implementos',
        },
        {
          id:9,
          name:'Camisa de la Selección Colombia',
          type:'Futbol',
          price:'50.00',
          src:require('../assets/img/shop/9.jpg'),
          keyword: 'Camisas',
        },
        {
          id:10,
          name:'Bolas de Ping-Pong',
          type:'Tenis',
          price:'34.00',
          src:require('../assets/img/shop/10.jpg'),
          keyword: 'Ping-Pong',
        },
        {
          id:11,
          name:'Caminadora',
          type:'Atletismo',
          price:'38.00',
          src:require('../assets/img/shop/11.jpg'),
          keyword: 'Caminadora',
        },
        {
          id:12,
          name:'Camisa de Equipo Chelsea',
          type:'Futbol',
          price:'25.00',
          src:require('../assets/img/shop/12.jpg'),
          keyword: 'Camisas',
        },



      ],
      model: null,
      search: null,
      tab: null,
    }),

    watch: {
      model (val) {
        if (val != null) this.tab = 0
        else this.tab = null
      },
      search (val) {
        // Items have already been loaded
        if (this.items.length > 0) return

        this.isLoading = true

        // Lazily load input items
        fetch('https://api.coingecko.com/api/v3/coins/list')
          .then(res => res.clone().json())
          .then(res => {
            this.items = res
          })
          .catch(err => {
            console.log(err)
          })
          .finally(() => (this.isLoading = false))
      },
    },
  }
</script>



