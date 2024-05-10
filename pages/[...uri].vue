<template>
  <main class="container mx-auto">
    <div class="py-16">
      <NuxtLink to="/" class="text-slate-100 text-lg uppercase flex mb-12">Back</NuxtLink>
      <div class="text-slate-100 text-xl mb-4">{{ new Date(data.date).toLocaleDateString() }}</div>
      <h1 class="text-8xl font-semibold text-slate-100">{{ data.title }}</h1>
    </div>
    <div class="">
      <article class="text-slate-100 mt-4 space-y-2" v-html="data.content"></article>
    </div>
  </main>
</template>

<script setup>

const route = useRoute();
const uri = route.params.uri.join('/');
const config = useRuntimeConfig();
const {data, pending, refresh, error} = await useFetch(config.public.wordpressUrl, {
  method: 'get',
  query: {
      query: `
      query MyQuery3($uri: String!) {
          nodeByUri(uri: $uri) {
              ... on Post {
                  id
                  title
                  date
                  content
              }
          }
      }
      `,
      variables: {
          uri: uri
      }
  },
  transform(data){
      return data.data.nodeByUri
  }
})


useHead({
  title: data.value.title
})
</script>
