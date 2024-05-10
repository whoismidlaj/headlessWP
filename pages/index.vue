<script setup lang="ts">
const route = useRoute()
const config = useRuntimeConfig();
const { data, refresh, pending } = await useFetch(config.public.wordpressUrl, {
 method: 'get',
 query: {
   query: `
     query NewQuery {
       posts(first:10){
         nodes {
           title
           date
           excerpt
           uri
         }
       }
     }`
},
transform(data){
return data.data.posts.nodes as Array<Record<'title' | 'date' | 'excerpt' | 'uri', string>>;
}
});
</script>

<template>
  <div class="container mx-auto">
    <div class="py-16">
      <h1 class="text-8xl font-semibold text-slate-100">Blogs</h1>
    </div>
    <div class="flex flex-col">
      <Post v-for="post in data" :key="post.uri" :post="post"></Post>
    </div>
  </div>
 </template>