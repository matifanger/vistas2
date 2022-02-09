<template>
    <div>
<div>
    <nav class="bg-white">
        <div class="px-8">
            <div class="flex items-center justify-between h-12">
                <div class=" flex items-center">
                    <div class="text-2xl">Logo</div>
                    <div class="hidden md:block">
                        <div class="ml-10 flex items-baseline space-x-4">
                            <NuxtLink to="/home" class="text-gray-800 px-3 py-2 rounded-md text-sm font-medium">
                                Home
                            </NuxtLink>
                            <NuxtLink to="/top-cupones" class="text-gray-800 px-3 py-2 rounded-md text-sm font-medium">
                                Top 20
                            </NuxtLink>
                        </div>
                    </div>
                </div>
                <div class="block">
            <!-- Search -->
            <div class="flex items-center justify-center">
                <div class="flex rounded">
                    <input type="text" class="px-4 py-2 w-60" placeholder="Buscar...">
                    <button class="flex items-center justify-center px-4">
                        <svg class="w-6 h-6 text-gray-600" fill="currentColor" xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 24 24">
                            <path
                                d="M16.32 14.9l5.39 5.4a1 1 0 0 1-1.42 1.4l-5.38-5.38a8 8 0 1 1 1.41-1.41zM10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z" />
                        </svg>
                    </button>
                    </div>
            </div>
                </div>
                <div class="-mr-2 flex md:hidden">
                    <button @click="turnMenu()" class="text-gray-800 hover:text-gray-300 inline-flex items-center justify-center p-2 rounded-md focus:outline-none">
                        <svg width="20" height="20" fill="currentColor" class="h-8 w-8" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg">
                            <path d="M1664 1344v128q0 26-19 45t-45 19h-1408q-26 0-45-19t-19-45v-128q0-26 19-45t45-19h1408q26 0 45 19t19 45zm0-512v128q0 26-19 45t-45 19h-1408q-26 0-45-19t-19-45v-128q0-26 19-45t45-19h1408q26 0 45 19t19 45zm0-512v128q0 26-19 45t-45 19h-1408q-26 0-45-19t-19-45v-128q0-26 19-45t45-19h1408q26 0 45 19t19 45z">
                            </path>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div v-show="showMenu" class="md:hidden absolute w-full z-50 text-white text-center bg-gray-500">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <NuxtLink to="/home" class="text-white block px-3 py-2 rounded-md text-base font-medium">
                    Home
                </NuxtLink>
                <NuxtLink to="/top-cupones" class="text-white block px-3 py-2 rounded-md text-base font-medium">
                    Top 20
                </NuxtLink>
            </div>
        </div>
    </nav>
</div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                showMenu: false,
            }
        },
        methods: {
            turnMenu() {
                this.showMenu = !this.showMenu
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>