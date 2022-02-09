<template>
    <div v-if="data != ''" class="overflow-x-hidden">
      <div class="max-w-screen-2xl mx-auto" style="width:95%">
        <Header />
        <div class="text-center mt-7">
        <h1 class="text-lg font-bold">{{data.page.title}}</h1>
        <h2 class="mt-3">{{data.page.subtitle}}</h2>
        </div>

      <!-- tabs -->
      <article class="mt-5">
        <div class="bg-white">
          <div class="font-bold text-lg">Tabas</div>
                        <nav class="tabs flex flex-col sm:flex-row text-sm">
                          <ul class="flex py-4 pr-5">
                            <li v-for="(tab, key) in Object.keys(data.data.tabs)" :key="key" @click="currentTab(key)" 
                          :class="showTab == key ? 'bg-yellow-700 active text-white font-bold': ''"
                          class="p-1 px-5">
                          <button class="mt-1">
                            {{tab}}
                          </button>
                          </li>
                          </ul>
                        </nav>
                    </div>
                    <div v-for="(tab, key, index) in data.data.tabs" :key="key">
                        <div class="tab-content active text-black">
                            <div v-show="showTab == index">
                                <div v-for="(item,key) in tab" :key="key">
                                  <div class="w-full mb-3">
                                    <div>
                                        <div class="border border-1 shadow flex items-center justify-between">
                                            <div class="flex py-5 px-5">
                                                <div :style="`background-color: ${item.shop.background}`" 
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
              </div>
      </article>


      </div>
      <Footer />
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
    data() {
      return {
        data: '',
        showTab: 0,
        tabValues: [],
      }
    },
    mounted() {
      axios.get('http://localhost:80/home').then(res => {
      console.log(res.data)
      this.data = res.data
      })
    },
    methods: {
      currentTab(key) {
        this.showTab = key
      },
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
