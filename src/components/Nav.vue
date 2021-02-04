<template>
  <div
    class="w-full sticky top-0 py-4 px-6 flex items-center justify-between bg-dark"
  >
    <div class="flex items-center">
      <button class="rounded-full bg-black w-8 h-8 text-white mr-3">
        <i class="material-icons text-2xl">keyboard_arrow_left</i>
      </button>
      <button class="rounded-full bg-black w-8 h-8 text-white">
        <i class="material-icons text-2xl">keyboard_arrow_right</i>
      </button>
    </div>
    <div class="relative">
      <button
        @click="showDropDown = true"
        class="bg-light rounded-full py-1 px-2 flex items-center focus:outline-none"
      >
        <img src="myface.jpg" class="rounded-full h-6 w-6 mr-2" />
        <p class="text-white font-semibold text-xs mr-3">Ucheya Okereke</p>
        <i v-if="showDropDown === false" class="material-icons text-white"
          >arrow_drop_down</i
        >
        <i v-if="showDropDown === true" class="material-icons text-white"
          >arrow_drop_up</i
        >
      </button>
      <div
        v-if="showDropDown === true"
        class="absolute bg-light w-full rounded mt-1"
      >
        <button
          @click="showDropDown = false"
          class="w-full focus:outline-none text-sm py-2 text-lightest hover text-white border-b border-white opacity-75 hover:opacity-100"
        >
          Account
        </button>
        <button
          @click="showDropDown = false"
          class="w-full focus:outline-none text-sm py-2 text-lightest hover text-white border-b border-light opacity-75 hover:opacity-100"
        >
          Log Out
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Nav",
  data() {
    return {
      showDropDown: false,
    };
  },
};
</script>
<style>
</style>