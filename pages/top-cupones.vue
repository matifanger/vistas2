<template>
    <div v-if="data != ''" class="overflow-x-hidden">
      <div class="max-w-screen-2xl mx-auto" style="width:95%">
        <Header />
        <div class="mt-7 grid grid-cols-12">
            <aside class="col-span-3">
                <div class="grid grid-cols-3">
                    <div v-for="(item,key) in data.data.sidebar.shops" :key="key">
                    <div style="background-color: #ffffff" 
                            class="h-16 w-16 ma-5 object-center border border-1 mt-2 flex"> 
                            <img :src="item.logo[0].url" class="object-scale-down">
                    </div>
                    </div>
                 </div>
                  <div class="mt-6">
                       <span class="font-bold">Mejores cupones</span>
                       <div v-for="(item,key) in data.data.sidebar.discounts" :key="key">
                       </div>
                  </div>
            </aside>
            <section class="col-span-9">
                <div>
                <h1 class="text-lg font-bold">{{data.page.title}}</h1>
                <h2 class="mt-3">{{data.page.subtitle}}</h2>
                

                <div v-for="(item, key) in data.data.discounts" :key="key">
                        <div class="tab-content active text-black">

                                  <div class="w-full mb-3">
                                    <div>
                                        <div class="border border-1 shadow flex items-center justify-between">
                                            <div class="flex py-5 px-5">
                                                <div style="background-color: #ffffff" 
                                                  class="h-24 w-24 ma-5 object-center flex"> 
                                                    <img :src="item.shop.logo[0].url" class="object-scale-down">
                                                </div>
                                                <div class="ml-5"> 
                                                <span v-if="checkCodeOrCupon(item.title)"> 
                                                    <p class="font-bold text-xs" style="color: #EE5034"> CÓDIGO </p>
                                                  </span>
                                                <span v-else> 
                                                    <p class="font-bold text-xs" style="color: #001558"> OFERTA </p>
                                                 </span>
                                                  <div class="text-medium md:text-lg" >
                                                    {{item.title}}
                                                  </div>
                                                  <span class="rounded-lg bg-gray-200 text-gray-900 px-5">verificado</span>
                                                  </div>
                                                </div>
                                                <a :href="item.url" target="_blank">
                                                  <div v-if="checkCodeOrCupon(item.title)" style="background: #EE5034"
                                                  class="w-28 md:w-40 text-center mr-5 rounded py-2 px-9 text-white font-bold">
                                                  Ver Cupón
                                                  </div>
                                                  <div v-else style="background: #001558"
                                                  class="w-28 md:w-40 text-center mr-5 rounded py-2 px-9 text-white font-bold">
                                                  Ver Oferta
                                                  </div>
                                                </a>
                                            </div>
                                        </div>  
                        </div>
                    </div>
              </div>
                
                
                
                </div>
        </section>
        </div>
      </div>
      <Footer />
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'top-cupones',
    data() {
      return {
        data: '',
        showTab: 0,
        tabValues: [],
      }
    },
    mounted() {
      axios.get('http://localhost:80/top-cuponse').then(res => {
      console.log(res.data)
      this.data = res.data
      })
    },
    methods: {
      checkCodeOrCupon(title) {
        title = title.split(' ')
        var filteredTitle = title.filter(word => word.toLowerCase().includes('cupón') || word.toLowerCase().includes('código') )
        if (filteredTitle == 'cupón' || filteredTitle == 'Cupón') {
          return  false
        } else if (filteredTitle == 'código' || filteredTitle == 'Código') {
          return  true
        } else return ''
      }
    }
}
</script>

<style>
.active {
  background:#EE5034,
}
</style>
