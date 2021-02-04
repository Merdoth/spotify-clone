<template>
  <div id="app" class="bg-dark h-screen">
    <div class="flex" style="height: 88vh">
      <SideBar />
      <div class="w-full h-full relative overflow-y-scroll">
        <Nav />
        <Main :recents="recents" />
      </div>
    </div>
    <Footer :recents="recents" />
  </div>
</template>

<script>
import Nav from "./components/Nav.vue";
import SideBar from "./components/SideBar.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";
export default {
  name: "App",
  components: {
    Nav,
    SideBar,
    Main,
    Footer,
  },
  data() {
    return {
      recents: [
        {
          id: 1,
          img: "bts.png",
          title: "Dynamite",
          artist: "BTS",
          src: require("./assets/dynamite.mp3"),
        },
        {
          id: 2,
          img: "billie-eyelash.jpg",
          title: "Everything I Wanted",
          artist: "Billie Eilish",
          src: require("./assets/everything.mp3"),
        },
        {
          id: 3,
          img: "jesus-image.png",
          title: "This Is The Sound",
          artist: "Steffany Gretzinger",
          src: require("./assets/this-is-the-sound.mp3"),
        },
        {
          id: 4,
          img: "jeremy-bethel.png",
          title: "Miracles",
          artist: "Jeremy Riddle",
          src: require("./assets/miracles.mp3"),
        },
        {
          id: 5,
          img: "347aidan.png",
          title: "Dancing In My Room",
          artist: "347aidan",
          src: require("./assets/dancing.mp3"),
        },
        {
          id: 6,
          img: "myalbumcover.jpg",
          title: "Chasing Dreams",
          artist: "Meya Samuels",
          src: require("./assets/song.mp3"),
        },
      ],
    };
  },
};
</script>

<style>
#app {
}
</style>
