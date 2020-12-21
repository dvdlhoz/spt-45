<template>
  <v-app id="inspire">
    <v-app-bar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      app
      color="primary"
      dark
    >
<!--      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />-->

      <v-toolbar-title
        style="width: 350px"
      >
        <a href="/" class="white--text" style="text-decoration: none"> <v-avatar>
          <img src='../assets/logo.jpg'></img>
        </v-avatar>&nbsp;SpartanSports</a>
      </v-toolbar-title>
       

           
      <v-btn icon> <v-icon>mdi-arrow-left</v-icon> </v-btn>
     
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
            href="/shop"
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
      
        
      <v-spacer />
      
      <v-btn href="#" :title="facebookTooltip" icon>
        <v-icon> mdi-facebook </v-icon>
      </v-btn>
      <v-btn href="#" :title="instagramTooltip" icon>
        <v-icon>mdi-instagram</v-icon>
      </v-btn>
      <v-btn href="#" :title="twitterTooltip" icon>
        <v-icon>mdi-twitter</v-icon>
      </v-btn>
     
      <v-btn v-on="on" href="/cart" icon>
        <v-badge
          content="2"
          value="2"
          color="green"
          overlap
        >
          <v-icon>mdi-shopping</v-icon>
        </v-badge>      
      </v-btn>
      <v-btn v-on="on" href="/registration" icon>
      <v-icon> mdi-account-circle </v-icon>
      </v-btn>
       
    </v-app-bar>
    <v-content>
      <v-bottom-navigation
        :value="activeBtn"
        color="primary"
        horizontal
      >
        <a href="/" class="v-btn">
          <span>Home</span>
        </a>
        <v-menu open-on-hover offset-y>
          <template v-slot:activator="{ on }">
            <v-btn v-on="on">
              <span>Shop</span>
            </v-btn>
          </template>
          <v-card
            class="mx-auto"
            max-width="344"
            outlined
          >

            <v-list-item
              v-for="(categoria, index) in categorias"
              :key="index"
              @click=""
              href="/shop"
            >
              <v-list-item-title>{{ categoria.title }}</v-list-item-title>
            </v-list-item>

          </v-card>
        </v-menu>
        <a href="/product" class="v-btn">
          <span>Product</span>
        </a>
        <v-btn href="/blog">
          <span>Blog</span>
        </v-btn>
      </v-bottom-navigation>
    </v-content>
      <router-view/>
    <v-footer
      :padless="true"
    >
      <v-card
        flat
        tile
        width="100%"
        class="secondary white--text text-center"
      >
        <v-card-text>
          <v-btn
            class="mx-4 white--text"
            icon
          >
            <v-icon size="24px">mdi-home</v-icon>
          </v-btn>
          <v-btn
            class="mx-4 white--text"
            icon
          >
            <v-icon size="24px">mdi-email</v-icon>
          </v-btn>
          <v-btn
            class="mx-4 white--text"
            icon
          >
            <v-icon size="24px">mdi-calendar</v-icon>
          </v-btn>
           <v-btn
            class="mx-4 white--text"
            icon
          >
            <v-icon size="24px">mdi-delete</v-icon>
          </v-btn>

        </v-card-text>

        <v-card-text class="white--text pt-0">
         Un sueño no se hace realidad por arte de magia, necesita sudor, determinación y trabajo duro - Colin Powell. En SpartanSports brindamos productos de alta calidad para la práctica del deporte tanto a nivel profesional como recreativo, ofreciendo soluciones para las distintas necesidades,  utilizando una plataforma tecnológica que simplifique y facilite los procesos de las distintas áreas,  comprometidos a apoyar la salud mental y física de nuestro público..
        </v-card-text>

        <v-divider></v-divider>

        <v-card-text class="white--text">
          {{ new Date().getFullYear() }} — <strong>SpartanSports</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
   

    export default {
        data () {
            return {
                categorias: [
                    { title: 'Baloncesto' },
                    { title: 'Voleibol' },
                    { title: 'Tenis' },
                    { title: 'Futbol' },
                    { title: 'Natación' },
                ],
                activeBtn: 1,
                facebookTooltip: 'Follow us on Facebook',
                instagramTooltip: 'Follow us on Instagram',
                twitterTooltip: 'Follow us on Twitter',                
                messages: 0,
                search: null,
                show: false,
                value: '',
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
                          
                      }        
                  },

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
