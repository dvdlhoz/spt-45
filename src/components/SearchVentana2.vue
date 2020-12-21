<template>
  <div>
    <v-container>
      <v-treeview
        :items="products"
        :search="search"
        :filter="filter"
        :open.sync="open"
      >
        <template v-slot:prepend="{ product }">
          <v-icon
            v-if="product.name"
            v-text="`mdi-${product.id === 1 ? 'home-variant' : 'folder-network'}`"
          ></v-icon>
        </template>
      </v-treeview>
    </v-container>
  </div>
</template>

<script>
export default {
    data: () => ({
       products:[
                {
                    id:1,
                    name:'Gafas',
                    type:'Natación',
                    price:'18.00',
                    src:require('../assets/img/shop/1.jpg')
                },
                {
                    id:2,
                    name:'Balón Mikasa ',
                    type:'Voleibol',
                    price:'40.00',
                    src:require('../assets/img/shop/2.jpg')
                },
                {
                    id:3,
                    name:'Zara limited...',
                    type:'Denim',
                    price:'25.00',
                    src:require('../assets/img/shop/3.jpg')
                },
                {
                    id:4,
                    name:'Balon Adidas',
                    type:'Futbol',
                    price:'30.00',
                    src:require('../assets/img/shop/4.jpg')
                },
                {
                    id:5,
                    name:'Zapatos',
                    type:'Atletismo',
                    price:'50.00',
                    src:require('../assets/img/shop/5.jpg')
                },
                {
                    id:6,
                    name:'Raquetas',
                    type:'Tenis',
                    price:'34.00',
                    src:require('../assets/img/shop/6.jpg')
                },
                {
                    id:7,
                    name:'Balón',
                    type:'Baloncesto',
                    price:'38.00',
                    src:require('../assets/img/shop/7.jpg')
                },
                {
                    id:8,
                    name:'Rodilleras',
                    type:'Implementos deportivos',
                    price:'25.00',
                    src:require('../assets/img/shop/8.jpg')
                },{
                    id:9,
                    name:'Camisa de la Selección Colombia',
                    type:'Futbol',
                    price:'50.00',
                    src:require('../assets/img/shop/9.jpg')
                },
                {
                    id:10,
                    name:'Bolaas de Ping-Pong',
                    type:'Tenis',
                    price:'34.00',
                    src:require('../assets/img/shop/10.jpg')
                },
                {
                    id:11,
                    name:'Caminadora',
                    type:'Atletismo',
                    price:'38.00',
                    src:require('../assets/img/shop/11.jpg')
                },
                {
                    id:12,
                    name:'Camisa de Equipo Chelsea',
                    type:'Futbol',
                    price:'25.00',
                    src:require('../assets/img/shop/12.jpg')
                }
            ],
      open: [1, 2],
      search: null,
      caseSensitive: false,
    }),
    computed: {
      filter () {
        return this.caseSensitive
          ? (item, search, textKey) => item[textKey].indexOf(search) > -1
          : undefined
      },
    },
  }
</script>




