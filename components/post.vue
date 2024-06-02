<template>
  <div class="z-50 bottom-0 h-full w-full">
    <div class="py-2 w-full">
      <div class="flex items-center justify-between">
        <div class="flex items-center text-white">
          <img
            :src="post.image"
            alt="post-image"
            class="rounded-full h-[35px]"
          />
          <div class="ml-2 font-semibold text-[18px]">{{ post.name }}</div>
        </div>

        <div class="relative">
          <button
            @click="isDeleted"
            :disabled="!isDeleting"
            class="flex items-center text-white p-1 h-[24px] w-[24px] hover:bg-gray-800 rounded-full cursor-pointer"
            :class="isMenu ? 'bg-gray-800' : ''"
          >
            <Icon
              v-if="!isDeleting"
              name="bi:three-dots"
              size="18"
              color="#fff"
            />
            <Icon
              v-else
              name="eos-icons:bubble-loading"
              size="18"
              color="#fff"
            />
          </button>

          <div
            v-if="isMenu"
            class="absolute border border-gray-600 right-0 z-20 mt-1 rounded"
          >
            <button
              class="flex items-center gap-2 text-red-500 justify-between bg-black w-full pl-4 pr-3 py-1 hover:bg-green-900"
            >
              <div>Delete</div>
              <Icon name="solar:trash-bin-trash-broken" size="20" color="red" />
            </button>
          </div>
        </div>
      </div>

      <div class="relative flex items-center w-full">
        <div class="mx-auto w-[42px]">
          <div class="absolute ml-4 mt-1 top-0 w-[1px] bg-gray-700 h-full" />
        </div>

        <div
          class="bg-black rounded-lg text-sm w-full font-light w-[calc(100% - 50px)]"
        >
          <div class="py-2 text-gray-300">{{ post?.text }}</div>
          <img
            v-if="post && post?.picture"
            :src="post.picture"
            alt=""
            class="mx-auto w-full mt-2 pr-2 rounded"
          />

          <div class="absolute mt-2 ml-8 w-full">
            <button :disabled="isLiked" class="flex items-center gap-1">
              <Icon
                class="p-1 text-white hover:bg-gray-800 rounded-full cursor-pointer"
                name="mdi:cards-heart-outline"
                color="#fff"
                size="28"
              />
            </button>
            <div class="relative text-sm text-gray-500">
              <div>
                <span>4</span>
                likes
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="relative inline-block text-gray-500 pt-1 pb-1.5">
      <div class="flex items-center">
        <div class="flex items-center flex-wrap text-white gap-1 w-[42px]">
          <div class="flex gap-0 5">
            <img
              src="https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg"
              alt=""
              class="rounded-full h-[14px] mt-2"
            />
            <img
              src="https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg"
              alt=""
              class="rounded-full h-[17px]"
            />
          </div>
          <div class="flex items-center">
            <img
              src="https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg"
              alt=""
              class="rounded-full h-[11px] ml-4"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="h-[1px] bg-gray-800 w-full mt-3" />
  </div>
</template>

<script setup>
import { useUserStore } from "~/stores/user";

const user = useUserStore();

const runTimeConfig = useRuntimeConfig();

let isMenu = ref(false);
let isDeleting = ref(false);
let isLiked = ref(false);

const emit = defineEmits(["isDeleted"]);
const props = defineProps({
  post: Object,
});
</script>

<style>
</style>import type { Icon } from '#build/components';
