<template>
  <div>
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
          v-for="recent in recents"
          :key="recent.id"
          class="p-2 w-52 relative"
        >
          <div
            class="h-full w-full absolute flex items-end justify-end p-8 opacity-0 hover:opacity-100"
          >
            <button
              class="bg-green rounded-full h-10 w-10 flex items-center justify-center focus:outline-none"
            >
              <i
                v-if="!isPlaying"
                @click="play()"
                class="material-icons text-white text-2xl"
                >play_arrow</i
              >
            </button>
          </div>
          <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
            <img
              :src="`${recent.img}`"
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
          v-for="custom in customs"
          :key="custom.id"
          class="p-2 w-52 relative"
        >
          <div
            class="h-full w-full absolute flex items-end justify-end p-8"
            :class="isPlaying && custom.src == current.src ? 'playing' : 'song'"
          >
            <button
              class="bg-green rounded-full h-10 w-10 flex items-center justify-center focus:outline-none"
            >
              <i
                v-if="!isPlaying"
                @click="play(custom)"
                class="material-icons text-white text-2xl"
                >play_arrow</i
              >
              <i
                v-else
                @click="pause()"
                class="material-icons text-white text-2xl"
                >pause</i
              >
            </button>
          </div>
          <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
            <img
              :src="`${custom.img}`"
              class="w-full shadow mb-2"
              style="height: 20vh; object-fit: cover"
            />
            <h1
              class="text-sm font-semibol d text-white tracking-wide truncate ..."
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
</template>
<script>
export default {
  name: "Main",
  props: ["recents"],
  data() {
    return {
      index: 0,
      isPlaying: false,
      player: new Audio(),
      current: {},
      customs: [
        {
          id: 7,
          img: "billie-eyelash2.png",
          title: "I Had A Dream ",
          artist: "Billie Eilish",
          src: require("../assets/therefore.mp3"),
        },
        {
          id: 8,
          img: "jesus-image.png",
          title: "This Is The Sound",
          artist: "Steffany Gretzinger",
          src: require("../assets/this-is-the-sound.mp3"),
        },
        {
          id: 9,
          img: "jeremy-bethel.png",
          title: "Miracles",
          artist: "Jeremy Riddle",
          src: require("../assets/miracles.mp3"),
        },
        {
          id: 10,
          img: "myalbumcover.jpg",
          title: "Holy",
          artist: "Justin Bebier",
          src: require("../assets/holy.mp3"),
        },
        {
          id: 11,
          img: "bts.png",
          title: "Dynamite",
          artist: "BTS",
          src: require("../assets/dynamite.mp3"),
        },
        {
          id: 12,
          img: "347aidan.png",
          title: "Dancing In My Room",
          artist: "347aidan",
          src: require("../assets/dancing.mp3"),
        },
      ],
    };
  },
  methods: {
    play(song) {
      if (typeof song.id != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.index++;
          let songs = this.recents;
          if (this.index > songs.length - 1) {
            this.index = 0;
          }
          this.current = songs[this.index];
          this.play(this.current);
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
  },
};
</script>
<style lang="css">
.playing {
  display: block;
  opacity: 100;
}
.song {
  opacity: 0;
}
.song:hover {
  opacity: 100;
}
</style>