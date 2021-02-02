<template>
  <div id="app" class="bg-dark h-screen">
    <div class="flex" style="height: 88vh">
      <!-- side nav -->
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
          <img src="jesus-image.png" class="w-full" style="height: 31vh" />
        </div>
      </div>
      <!-- main content -->
      <div class="w-full h-full relative overflow-y-scroll">
        <!-- header -->
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
              <p class="text-white font-semibold text-xs mr-3">
                Ucheya Okereke
              </p>
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
        <!-- cards -->
        <div class="px-6 py-3">
          <div class="flex items-center justify-between">
            <h1
              class="pl-2 text-2xl font-semibold text-white tracking-wider hover:underline"
            >
              Recently Played
            </h1>
            <h2
              class="pr-8 pt-4 text-xs text-lightest uppercase tracking-wider hover:underline mb-3"
            >
              See All
            </h2>
          </div>
          <div class="w-full flex flex-wrap justify-evenly">
            <div
              v-for="(recent, index) in recents"
              :key="index"
              class="p-2 w-52 relative"
            >
              <div
                class="h-full w-full absolute flex items-end justify-end p-8 opacity-0 hover:opacity-100"
              >
                <div
                  class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
                >
                  <i class="material-icons text-white text-2xl">play_arrow</i>
                </div>
              </div>
              <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                <img
                  :src="`${recent.src}`"
                  class="w-full shadow mb-2"
                  style="height: 20vh; object-fit: cover"
                />
                <h1
                  class="text-sm font-semibold text-white tracking-wide truncate ..."
                >
                  {{ recent.title }}
                </h1>
                <h2 class="text-xs text-lightest tracking-wide pb-5">
                  {{ recent.artist }}
                </h2>
              </div>
            </div>
          </div>
        </div>
        <div class="px-6 py-3">
          <div class="pl-2">
            <h1
              class="text-2xl font-semibold text-white tracking-wider hover:underline"
            >
              Made for Ucheya
            </h1>
            <h2 class="text-sm text-lightest">
              Get better recommendations the more you listen.
            </h2>
          </div>
          <div class="w-full flex flex-wrap justify-evenly">
            <div
              v-for="(custom, index) in customs"
              :key="index"
              class="p-2 w-52 relative"
            >
              <div
                class="h-full w-full absolute flex items-end justify-end p-8 opacity-0 hover:opacity-100"
              >
                <div
                  class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
                >
                  <i class="material-icons text-white text-2xl">play_arrow</i>
                </div>
              </div>
              <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                <img
                  :src="`${custom.src}`"
                  class="w-full shadow mb-2"
                  style="height: 20vh; object-fit: cover"
                />
                <h1
                  class="text-sm font-semibold text-white tracking-wide truncate ..."
                >
                  {{ custom.title }}
                </h1>
                <h2 class="text-xs text-lightest tracking-wide pb-5">
                  {{ custom.artist }}
                </h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- play button aka footer -->
    <div
      class="w-full bg-light flex items-center justify-between px-3 border-t border-dark"
      style="height: 12vh"
    >
      <div class="flex items-center w-1/4">
        <div>
          <h1 class="text-sm text-white tracking-wide">
            Summer in the City - Remastered
          </h1>
          <h2 class="text-xs text-lightest tracking-wide">
            The Lovin' Spoonful
          </h2>
        </div>
        <i class="material-icons text-xl text-green mx-4">favorite</i>
        <i class="material-icons text-xl text-lightest hover:text-white"
          >picture_in_picture_alt</i
        >
      </div>
      <div class="flex flex-col justify-center w-2/4 items-center">
        <div class="flex items-center">
          <button class="text-lightest hover:text-white mx-5">
            <i class="material-icons text-lg">shuffle</i>
          </button>
          <button class="text-lightest hover:text-white">
            <i class="material-icons text-lg">skip_previous</i>
          </button>
          <button
            @click.prevent="playSong('song.mp3'), (pause = true)"
            class="rounded-full h-10 w-10 flex items-center justify-center mx-5 border-lightest border text-lightest focus:outline-none hover:text-white"
          >
            <i v-if="pause === false" class="material-icons">play_arrow</i
            ><i v-if="pause === true" class="material-icons">pause</i>
          </button>
          <button class="text-lightest hover:text-white">
            <i class="material-icons text-lg">skip_next</i>
          </button>
          <button class="text-lightest hover:text-white mx-5">
            <i class="material-icons text-lg">repeat</i>
          </button>
        </div>
        <div class="w-3/4 flex items-center justify-center mt-3">
          <p class="text-xs text-lightest mr-1">0.28</p>
          <div class="w-full h-1 rounded-full bg-dark flex items-center">
            <div class="h-1 rounded-full bg-green" style="width: 18%"></div>
            <div class="h-3 w-3 bg-white rounded-full -ml-1 shadow"></div>
          </div>
          <p class="text-xs text-lightest ml-1">2.40</p>
        </div>
      </div>
      <div class="flex items-center w-1/4 justify-end">
        <i class="material-icons text-lightest hover:text-white"
          >playlist_play</i
        >
        <i class="material-icons text-xl text-lightest mx-3 hover:text-white"
          >important_devices</i
        >
        <i class="material-icons text-xl text-lightest hover:text-white"
          >volume_up</i
        >
        <div
          class="w-20 ml-1 bg-lightest rounded-full h-1 hover:text-white"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
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
      showDropDown: false,
      pause: false,
      recents: [
        { src: "bts.png", title: "Dynamite", artist: "BTS" },
        {
          src: "billie-eyelash.jpg",
          title: "Everything I Wanted",
          artist: "Billie Eilish",
        },
        {
          src: "jesus-image.png",
          title: "This Is The Sound",
          artist: "Steffany Gretzinger",
        },
        {
          src: "jeremy-bethel.png",
          title: "Miracles",
          artist: "Jeremy Riddle",
        },
        {
          src: "347aidan.png",
          title: "Dancing In My Room",
          artist: "347aidan",
        },
        {
          src: "myalbumcover.jpg",
          title: "Chasing Dreams",
          artist: "Meya Samuels",
        },
      ],
      customs: [
        {
          src: "billie-eyelash2.png",
          title: "I Had A Dream ",
          artist: "Billie Eilish",
        },
        {
          src: "jesus-image.png",
          title: "This Is The Sound",
          artist: "Steffany Gretzinger",
        },
        {
          src: "jeremy-bethel.png",
          title: "Miracles",
          artist: "Jeremy Riddle",
        },
        { src: "myalbumcover.jpg", title: "Radios", artist: "By Spotify" },
        { src: "bts.png", title: "Dynamite", artist: "BTS" },
        {
          src: "347aidan.png",
          title: "Dancing In My Room",
          artist: "347aidan",
        },
      ],
    };
  },
  methods: {
    playSong(song) {
      if (song) {
        let audio = new Audio(song);
        return audio.play();
      }
    },
  },
};
</script>

<style>
#app {
}
</style>
