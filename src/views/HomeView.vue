<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <div>
    <v-container>
      <br>
      <div style="text-align: center">
        <h1>Vue Card Produto</h1>
        <br>
      </div>
      <v-row>
        <v-col cols="12"><h3>Com todas as opções</h3></v-col>
        
        <v-col cols="12" v-for="(item, index) in 1" :key="'mais_vendidos_'+index">
            <VCardProduto :item="lista[index]" @goTo="gotTo" :toggle_exclusive="true">
              <template v-slot:extra_txt_valor>
                tem ate <b>12x</b> de <span style='color: red'>1,20</span>
              </template>
            </VCardProduto>
        </v-col>
        
        
        <v-col cols="12"><h3>Com todas as opções</h3></v-col>
        
        <v-col col="12" sm="6" md="4" lg="3" v-for="(item, index) in lista" :key="'mais_vendidos_'+index">
            <VCardProduto :item="item" @goTo="gotTo" >
              <template v-slot:extra_txt_valor>
                tem ate <b>12x</b> de <span style='color: red'>1,20</span>
              </template>
            </VCardProduto>
       
        </v-col>
        
       
        
        <v-col cols="12"><h3>Sem instock,  Sem o cabeçalho, Sem parcelas</h3></v-col>
        <v-col col="12" sm="6" md="4" lg="3" v-for="(item, index) in lista" :key="'mais_vendidos_'+index">
          <VCardProduto :item="item" @goTo="gotTo"   :show_instock="false"  :show_header="false" ></VCardProduto>
        </v-col>
        
        <v-col cols="12"><h3>Sem instock,  Sem o cabeçalho, Sem parcelas, Sem avaliação</h3></v-col>
        <v-col col="12" sm="6" md="4" lg="3" v-for="(item, index) in lista" :key="'mais_vendidos_'+index">
          <VCardProduto :item="item" @goTo="gotTo" :show_instock="false"  :show_header="false" :show_rating="false" >
          </VCardProduto>
        </v-col>
        
      
      
       
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import VCardProduto from '../components/VCardProduto.vue';

export default defineComponent({
  name: 'HomeView',
  data:()=>({
    lista:[]
 
  
  }),
  components: {
    VCardProduto,
  },

   methods: {
     gotTo(item){
         console.log('goTo:',item);
       // var titulo = this.item.titulo.replaceAll(' ', '-').toLowerCase()
       // router.push({name: this.routeName, params: {item: titulo}}).catch(err => {
       // })
     },
   },
  mounted(){
    for (var i = 0; i < 4; i++) {
      this.lista.push(
        {
          src: `https://picsum.photos/400/200?random=${i + 1}`,
          src2: `https://picsum.photos/400/200?random=${i + 2}`,
          valor: parseFloat(Math.random()*1000+20).toFixed(2),
          rating: parseFloat(Math.random()*4+1).toFixed(2),
          titulo: 'Produto ' + i + '-Est laborum nihil vel labore suscipit',
          descricao: 'Aut asperiores cumque quo incidunt iure sed itaque corrupti. Ex nulla laboriosam et laboriosam tenetur et iusto atque aut aspernatur nihil cum iure sequi cum totam iste qui Quis necessitatibus',
        }
      )
    
    }
  
  }
});
</script>
