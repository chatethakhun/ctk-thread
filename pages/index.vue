<template>
    <MainLayout>
        <section id="IndexPage" class="w-full overflow-auto text-white">
            <div class="mx-auto max-w-[500px] overflow-hidden">
                <div  id="Posts" class="px-4 max-w-[600px] mx-auto" >
                    <div v-if="isPosts"  v-for="post in posts" :key="post">
                    {{ post }}</div>
                </div>
            </div>
        </section>
    </MainLayout>
</template>

<script setup>
import MainLayout from '~/layouts/MainLayout.vue';
import { useUserStore } from '~/stores/user';

const user = useUserStore();

let posts = ref([])
let isPosts = ref(true)
let isLoading = ref(false)

onBeforeMount( () => {
    posts.value = [{
        name: "John Week dev",
        image: "https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg",
        text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla nec purus feugiat, molestie ipsum et, consequat nibh. Etiam non elit dui. Nulla nec purus feugiat, molestie ipsum et, consequat nibh. Etiam non elit dui.",
        picture: "https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg",
    }]
})
</script>