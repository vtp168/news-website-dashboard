<template>
  <div class="flex flex-col md:flex-row gap-4">
    <!-- Center Content (News Cards) -->
    <div class="flex-1 flex flex-col gap-2 mt-20">
      <div class="container mx-auto px-2 py-2 border-b-red-400 border-b-2 mb-4">
        <h1 class="text-lg">{{title}}</h1>
      </div>
      <div class="flex flex-col md:flex-row gap-2">
       
        <!-- 📋 News List (Left) -->
        <div class="flex-1 space-y-3">
          <div
            v-for="(item, index) in posts"
            :key="index"
            class="flex flex-row bg-white p-1 border-b-2 border-gray-100 overflow-hidden"
          >
          <router-link :to="`/article/detail/${item.id}`">
               <img :src="imgPath+'/'+item.thumbnail" alt="News Image" class="w-64 h-40 object-cover flex-shrink-0"/>
          </router-link>
           
            <div class="p-2 flex-1 ">
               <router-link :to="`/article/detail/${item.id}`">
                <h3 class="text-md font-semibold text-gray-800">{{ item.title }}</h3>
                <p class="text-gray-600 mt-1 text-sm">{{ truncate(item.body, 200) }}</p>
               </router-link>
              
              <!-- <p class="text-gray-600 mt-1">{{ item.body }}</p> -->
            </div>
          </div>
        </div>
      </div>
      <div class="container mx-auto rounded-2xl border-gray-100 border-2 mb-4 justify-center">
        <h1 class="text-md mb-1 text-center"><router-link to="/category">មើលបន្ថែម</router-link></h1>
      </div>
    </div>
    <!-- Right Side (Advertisement) -->
    <div class="md:block md:w-1/5">
      <div class="bg-gray-100 h-full flex items-center justify-center p-4 rounded shadow">
        <span class="text-gray-500 text-center">ផ្សព្វផ្សាយទីនេះ</span>
      </div>
    </div>
  </div>

</template>

<script setup>
import { ref } from "vue";

let imgPath=import.meta.env.VITE_IMAGE_PATH;

defineProps({
  posts: {
    type: Array,
    default: () => []
  },
  title: {
    type: String,
    default: 'Category News'
  }
});

function truncate(text, length = 200) {
  if (!text) return ''
  const div = document.createElement('div')
  div.innerHTML = text
  const plainText = div.textContent || div.innerText || ''
  return plainText.length > length
    ? plainText.slice(0, length) + '...'
    : plainText
}
</script>