<template>
<div class="max-w-screen-xl mx-auto px-4">
  <Loading :active="isLoading" :can-cancel="false" :is-full-page="true" :opacity="0.9" />
  <!-- <div class="flex justify-between mt-20">
    <div class="mx-auto table text-center text-sm">
        <a class="uppercase" href="#">Advertisement</a>
        <a href="#">
          <img src="@/img/ads/ads_728.jpg" alt="advertisement area">
        </a>
    </div>
  </div> -->
<CateogoryNewsCardList :title="title" :posts="posts"/>
</div>

</template>


<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import Loading from 'vue-loading-overlay'
import 'vue-loading-overlay/dist/css/index.css'
import { useRoute } from 'vue-router'

import CateogoryNewsCardList from '@/views/public/post-category/CategoryNewsCardList.vue';

const isLoading = ref(false)

const posts = ref([]);
const title = ref(''); // Category title
//const slug = ref('local-news'); // Default category slug
const route = useRoute();


const fetchPosts = async () => {
  try {
    //const res = await axios.get("http://127.0.0.1:8000/api/articles");
   isLoading.value=true;
  //  let slug = ref(route.params.slug || 'local-news'); // Get slug from route params or
  //  console.log("Category Slug:", slug);
    const res = await axios.get(`${import.meta.env.VITE_API_URL}/articles/category/${route.params.slug}`);
    if (res?.data) {
      isLoading.value=false;
      posts.value = res.data.posts;
      title.value = res.data.category; // Assuming the API returns category name
    }
  } catch (err) {
    console.error("Error fetching posts:", err);
    isLoading.value=false;
  }
};

onMounted(() => {
  fetchPosts();
});



</script>
