<template>
  <div
    class="w-full bg-light flex items-center justify-between px-3 border-t border-dark absolute"
    style="height: 12vh"
  >
    <div class="flex items-center w-1/4">
      <div>
        <h1 class="text-sm text-white tracking-wide" v-bind:recents="recents">
          {{ current.title || recents[index].title }}
        </h1>
        <h2 class="text-xs text-lightest tracking-wide">
          {{ current.artist || recents[index].artist }}
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
        <button
          @click="next"
          class="text-lightest hover:text-white focus:outline-none"
        >
          <i class="material-icons text-lg">skip_previous</i>
        </button>
        <div
          class="rounded-full h-10 w-10 flex items-center justify-center mx-5 border-lightest border text-lightest focus:outline-none hover:text-white"
        >
          <button
            v-if="!isPlaying"
            :recents="recents"
            @click="play({ recents })"
            class="focus:outline-none mt-1"
          >
            <i class="material-icons">play_arrow</i>
          </button>
          <button v-else @click="pause()" class="focus:outline-none mt-1">
            <i class="material-icons">pause</i>
          </button>
        </div>
        <button
          @click="next"
          class="text-lightest hover:text-white focus:outline-none"
        >
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
      <i class="material-icons text-lightest hover:text-white">playlist_play</i>
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
</template>
<script>
export default {
  name: "Footer",
  props: ["recents"],
  data() {
    return {
      index: 0,
      current: {},
      isPlaying: false,
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
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
    next() {
      let songs = this.recents;
      this.index++;
      if (this.index > songs.length - 1) {
        this.index = 0;
      }
      this.current = songs[this.index];
      this.play(this.current);
    },
    prev() {
      let songs = this.recents;
      this.index--;
      if (this.index < 0) {
        this.index = songs.length - 1;
      }
      this.current = songs[this.index];
      this.play(this.current);
    },
    created() {
      let songs = this.recents;
      this.current = songs[this.index];
      this.player.src = this.current.src;
    },
  },
};
</script>
<style>
</style>