<template>
  <div class="w-56 bg-black h-full flex-none">
    <div class="p-6">
      <img
        src="spotifyLogoWhite.png"
        class="h-10"
        style="filter: brightness(0) invert(1)"
      />
    </div>
    <div class="mx-2 mb-5">
      <button
        v-for="page in pages"
        :key="page.id"
        @click="setID = page.id"
        :class="`w-full focus:outline-none text-sm font-semibold rounded px-3 py-2 flex items-center justify-start ${
          setID === page.id ? 'bg-light text-white' : 'text-lightest'
        }`"
      >
        <i class="material-icons mr-3">{{ page.icon }}</i>
        <p>{{ page.name }}</p>
      </button>
    </div>
    <div class="mx-5">
      <h1 class="mb-3 text-xs text-lightest tracking-widest uppercase">
        Playlists
      </h1>
      <button
        class="flex items-center justify-start opacity-75 hover:opacity-100 mb-2"
      >
        <img src="add.png" class="h-8 w-8 mr-3 bg-plain-white" />
        <p class="text-sm text-white font-semibold">Create Playlist</p>
      </button>
      <button
        class="flex items-center justify-start opacity-75 hover:opacity-100"
      >
        <img src="favorites.png" class="h-8 w-8 mr-3 bg-plain-white" />
        <p class="text-sm text-white font-semibold">Liked Songs</p>
      </button>
      <div class="h-px w-full bg-light my-3"></div>
    </div>
    <div class="mx-5">
      <div class="w-full h-10 overflow-y-scroll">
        <p
          v-for="(album, index) in albums"
          :key="index"
          class="text-sm text-lightest hover:text-white py-1"
        >
          {{ album.name }}
        </p>
      </div>
      <button
        class="flex items-center justify-start text-lightest hover:text-white py-2"
      >
        <i
          class="material-icons mr-3 rounded-full border text-sm border-lightest"
          >arrow_downward</i
        >
        <p class="text-sm font-semibold">Install App</p>
      </button>
    </div>
    <div class="relative pt-6">
      <div
        class="w-full h-full flex justify-end items-start opacity-0 hover:opacity-100 absolute p-2"
      >
        <div class="bg-black rounded-full w-6 h-6">
          <i class="material-icons text-white">keyboard_arrow_down</i>
        </div>
      </div>
      <img src="jesus-image.png" class="w-full" style="height:40vh" />
    </div>
  </div>
</template>
<script>
export default {
  name: "SideBar",
  data() {
    return {
      pages: [
        { id: "home", name: "Home", icon: "home" },
        { id: "search", name: "Search", icon: "search" },
        { id: "library", name: "Your Library", icon: "bar_chart" },
      ],
      setID: "home",
      albums: [
        { name: "Drive" },
        { name: "miah" },
        { name: "All New Indie" },
        { name: "Mellow" },
        { name: "Classic Road Trip Songs" },
        { name: "Jesus Image Radio" },
      ],
    };
  },
};
</script>
<style>
</style>