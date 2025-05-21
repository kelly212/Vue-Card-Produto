<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
			<div class="card">
						<v-card :theme="theme" :class="classe " :elevation="elevation" class="boxImagem">
									<v-card-text>
												<v-row no-gutters>
															<v-col cols="12" sm="12" :md="toggle_exclusive ? '3' : '12'"
																						class="boxImagem" @click="goTo()" style="cursor: pointer">
																		<!--IMAGEM 1-->
																		<v-img loading="lazy" defer class="imagem1" :src="item.src" cover
																									width="100%"
																									:height="toggle_exclusive ? '100%' : '150px'" :alt="item.titulo">
																					<v-chip v-if="show_instock" variant="flat" size="small" :color="color_instock" text-color="white" label>
																								{{text_instock}}
																					</v-chip>
																					
																					<template v-slot:placeholder>
																								<v-row align="center" class="fill-height ma-0" justify="center">
																											<v-progress-circular color="verde" indeterminate></v-progress-circular>
																								</v-row>
																					</template>
																		</v-img>
																		<!--IMAGEM 2-->
																		<v-img loading="lazy" defer class="imagem2" :src="item.src2" cover
																									width="100%"
																									:height="toggle_exclusive ? '100%' : '150px'" :alt="item.titulo">
																					
																					<template v-slot:placeholder>
																								<v-row align="center" class="fill-height ma-0" justify="center">
																											<v-progress-circular color="verde" indeterminate></v-progress-circular>
																								</v-row>
																					</template>
																					
																					<div>
																								<v-chip v-if="show_instock" variant="flat" size="small" :color="color_instock" text-color="white" label>
																											{{text_instock}}
																								</v-chip>
																					</div>
																		
																		</v-img>
															</v-col>
															<v-col cols="12" sm="12" :md="toggle_exclusive ? '9' : '12'">
																		<v-card flat>
																					<v-card-text style=" padding: 0 15px 0 15px; text-align: left; cursor: pointer" @click="goTo()">
																								<small :style="'color:'+color_header" v-if="show_header">{{text_header}}</small>
																								<p style="font-weight: bold; font-size: 16px">{{item.titulo}}</p>
																								
																								<small class="font_size_14">
																											{{cortarString(item.descricao, toggle_exclusive ? 300 : 60)}}
																								</small>
																								
																								
																								<div class="text-left">
																											<div v-if="show_valor">
																														<p style="font-size: 1.5rem; font-weight: 500">R$ {{item.valor}}</p>
																														<slot name="extra_txt_valor"></slot>
																											
																											</div>
																											<v-rating v-if="show_rating" density="compact" hide-details v-model="item.rating" bg-color="orange-lighten-1"
																																					:color="color_rating"
																																					size="x-small"></v-rating>
																								</div>
																					</v-card-text>
																					<v-card-actions v-if="show_buy" class="justify-center" style=" padding: 0 15px 0 15px; ">
																								<v-btn :color="color_buy" class="ma-2" variant="flat" block @click="goTo()" name="agora">
																											<v-icon start aria-label="cart">mdi-cart</v-icon>
																											{{text_buy}}
																								</v-btn>
																					</v-card-actions>
																		</v-card>
															
															</v-col>
												</v-row>
									
									</v-card-text>
						</v-card>
			</div>
</template>

<script defer>
   /* eslint-disable */
   // import router from '../router/router'

   export default {
      name: "VCardProduto",

      props: {
         item: {default: []},
         theme: {theme: 'light'},
         classe: {default: ''},
         routeName: {default: 'DetalheItem'},
         toggle_exclusive: {default: false},
         elevation: {default: 1},
         /*instock*/
         show_instock: {default: true},
         color_instock: {default: 'orange'},
         text_instock: {default: 'IN STOCK'},
         /*btn comprar*/
         show_buy: {default: true},
         color_buy: {default: 'green'},
         text_buy: {default: 'Comprar Agora'},
         /*rating*/
         show_rating: {default: true},
         color_rating: {default: 'orange'},
         /*header*/
         show_header: {default: true},
         color_header: {default: 'teal'},
         text_header: {default: 'Cabeçaho'},
         /*valor*/
         show_valor: {default: true},


      },
      components: {},
      data: () => ({
         rating: 3,
         messages: [
            {
               from: 'You',
               message: `Sure, I'll see you later.`,
               time: '10:42am',
               color: 'deep-purple-lighten-1',
            },
         ],
         defaultImage: 'https://picsum.photos/400/200?image=15',
         hoverImage: 'https://picsum.photos/400/200?image=25',
         currentImage: 'https://picsum.photos/400/200?image=15',

      }),
      methods: {
         validarCampo(campo) {
            if (campo !== undefined && campo !== null && campo !== '') {
               return true
            } else {
               return false
            }
         },
         cortarString(str, tam) {
            if (this.validarCampo(str)) {
               if (str.length > tam) {
                  str = str.slice(0, tam) + '...'
               }
            }
            return str
         },
         goTo() {
            // var titulo = this.item.titulo.replaceAll(' ', '-').toLowerCase()
            this.$emit('goTo', this.item)
            // router.push({name: this.routeName, params: {item: titulo}}).catch(err => {
            // })

         }
      },
      created() {
      },
      mounted() {
      },
      computed: {},
      watch: {}
   }
</script>

<style scoped>
			.imagem1 {
						display: flex;
			}
			
			.boxImagem:hover .imagem1 {
						display: none;
			}
			
			.imagem2 {
						opacity: 0;
						visibility: hidden;
						display: none;
			}
			
			.imagem2 img {
			}
			
			.boxImagem:hover .imagem2 {
						visibility: visible;
						opacity: 1;
						-webkit-transform: translateY(0px);
						transform: translateY(0px);
						display: flex;
			}
			
			.card {
						transition: transform 0.2s ease-in-out;
			}
			
			.card:hover {
						transition: 0.2s ease-in-out;
						transform: translateY(-15px);
			}

</style>
