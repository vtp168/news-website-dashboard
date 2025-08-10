<template>
  <AdminLayout>
    <PageBreadcrumb :pageTitle="currentPageTitle" />
    <div class="space-y-5 sm:space-y-6">
      <ComponentCard>
        <Loading :active="isLoading" :can-cancel="false" :is-full-page="true"/>
        <PostTable :posts="posts" @refresh="fetchPosts" />
      </ComponentCard>
    </div>
  </AdminLayout>
</template>

<script setup>

import { onMounted, ref } from "vue";
import PageBreadcrumb from "@/components/admin/common/PageBreadcrumb.vue";
import AdminLayout from "@/components/admin/layout/AdminLayout.vue";
import ComponentCard from "@/components/admin/common/ComponentCard.vue";
import PostTable from "@admin/Posts/PostTable.vue";
import axios from "axios";
import Loading from 'vue-loading-overlay'
import 'vue-loading-overlay/dist/css/index.css';

const isLoading = ref(false)


const currentPageTitle = ref("All Post");

const posts= ref([]);

// for edit post
onMounted(() => {
  fetchPosts()

})

const fetchPosts = async (id) => {
  try
  {
    isLoading.value = true
    const res  = await axios.get(`${import.meta.env.VITE_API_URL}/posts`)
    if(res)
    {
        posts.value=res.data
        isLoading.value = false
        console.log(res.data)
    }
  }
  catch (err) {
    isLoading.value = false
    console.error(err)
  }
  }

  </script>