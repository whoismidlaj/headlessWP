<template>
    <NuxtLink :to='post.uri'>
        <div class="py-8
        px-2
        text-slate-100
        border-b
        border-zinc-900
        hover:bg-zinc-900"
        >
            <div>
                <h2 class="font-semibold text-2xl">{{ post.title }}</h2>
                <p>{{ new Date(post.date).toLocaleDateString() }}</p>
            </div>
        </div>
    </NuxtLink>
 </template>
 <script setup lang="ts">
 const props = defineProps<{
    post: Record<'title' | 'date' | 'excerpt' | 'uri', string>
 }>();
 
 </script>
 