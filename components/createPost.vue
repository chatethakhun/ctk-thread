<template>
  <div
    id="CreatePost"
    class="fixed z-50 bottom-0 h-full w-full overflow-hidden"
  >
    <div class="bg-black h-full w-full text-white overflow-auto">
      <div
        class="flex items-center justify-start py-4 max-w-[500px] mx-auto border-b border-b-gray-700"
      >
        <button @click="user.isMenuOverlay = false" class="rounded-full px-2">
          <Icon name="mdi:close" size="25" />
        </button>
        <div class="font-semibold text-[16px]">New Thread</div>
      </div>

      <div
        id="Post"
        class="z-40 bottom-0 max-h-[100vh-200px] w-full px-3 max-w-[500px] mx-auto"
      >
        <div class="py-2 w-full">
          <div class="flex items-center">
            <div class="flex items-center text-white">
              <img
                class="rounded-full h-[35px]"
                src="https://picsum.photos/id/223/50"
                alt="Image"
              />
              <div class="ml-2 font-semibold text-[18px]">John Wick</div>
            </div>
          </div>

          <div class="relative flex items-center w-full">
            <div class="mx-auto w-[42px]">
              <div
                class="absolute ml-4 mt-1 top-0 w-[1px] h-full bg-gray-700"
              />
            </div>
            <div
              class="bg-black rounded-lg w-[calc(100%-50px)] text font-light"
            >
              <div class="pt-2 text-gray-300 bg-black w-full">
                <textarea
                  id="textarea"
                  style="resize: none"
                  v-model="text"
                  @input="adjustTextareaHeight"
                  class="w-full bg-black focus:outline-none"
                  outline-none
                  placeholder="Start a new thread..."
                />
              </div>

              <div class="w-full">
                <div class="flex flex-col gap-2 py-2">
                  <div v-if="fileDisplay">
                    <img
                      :src="fileDisplay"
                      class="mx-auto w-full mt-2 mr-2 rounded-lg"
                    />
                  </div>

                  <label for="fileInput">
                    <Icon
                      name="clarity:paperclip-line"
                      size="25"
                      color="#fff"
                    />
                    <input
                      ref="file"
                      type="file"
                      id="fileInput"
                      @input="onChange"
                      hidden
                      accept=".jpg,.jpeg,.png"
                    />
                  </label>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <button
        v-if="text"
        :disabled="isLoading"
        class="fixed bottom-0 font-bold text-lg w-full p-2 bg-black inline-block float-right p-4 border-t border-t-gray-700"
        :class="isLoading ? 'text-gray-600' : 'text-blue-600'"
      >
        <div v-if="!isLoading">Post</div>
        <div v-else class="flex items-center gap-2 justify-center">
          <Icon name="eos-icons:bubble-loading" size="25" />
          <div>Please wait...</div>
        </div>
      </button>
    </div>
  </div>
</template>

<script setup>
import { v4 as uuidv4 } from "uuid";
import { useUserStore } from "~/stores/user";
const user = useUserStore();

const text = ref(null);
const isLoading = ref(false);
let file = ref(null);
let fileDisplay = ref(null);
let fileData = ref(null);

const adjustTextareaHeight = (e) => {
  const textarea = document.getElementById("textarea");
  textarea.style.height = "auto";
  textarea.style.height = textarea.scrollHeight + "px";
};

const onChange = (e) => {
  fileDisplay.value = URL.createObjectURL(file.value.files[0]);
  fileData.value = file.value.files[0];
};

const clearData = () => {
  text.value = null;
  file.value = null;
  fileDisplay.value = null;
  fileData.value = null;
};
</script>

<style>
</style>