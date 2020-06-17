<template>
  <div class="music-card">
    <header class="navbar">
      <h1>
        <img :src="logoSrc" alt="headphone logo" class="img-logo" />
        <span>Qurany</span>
      </h1>
    </header>
    <main>
      <section class="player">
        <h1 class="quran-title">
          {{ currentQuran.title }} - <span>{{ currentQuran.artist }}</span>
        </h1>
        <div class="controls">
          <button class="prev" @click="prev">
            <img
              :src="prevImage"
              alt="previous logo"
              class="player-control-logo"
            />
          </button>
          <button class="play" v-if="!isPlaying" @click="play">
            <img :src="playImage" alt="play logo" class="play-control-logo" />
          </button>
          <button class="pause" v-else @click="pause">
            <img :src="pauseImage" alt="pause logo" class="play-control-logo" />
          </button>
          <button class="next" @click="next">
            <img :src="nextImage" alt="next logo" class="player-control-logo" />
          </button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import listOfQuran from "./../quran";

export default {
  name: "home",
  data: function() {
    return {
      currentQuran: {},
      logoSrc: require("./../assets/images/headphones.png"),
      prevImage: require("./../assets/images/previous.png"),
      playImage: require("./../assets/images/play.png"),
      nextImage: require("./../assets/images/next.png"),
      pauseImage: require("./../assets/images/pause.png"),
      currentIndex: 0,
      isPlaying: false,
      listOfQuran,
      player: new Audio()
    };
  },
  methods: {
    play: function(quran) {
      if (typeof quran.src !== "undefined") {
        this.currentQuran = quran;
        this.player.src = this.currentQuran.src;
      }
      this.player.play();
      this.player.addEventListener(
        "ended",
        function() {
          this.currentIndex++;
          if (this.currentIndex > this.listOfQuran.length - 1) {
            this.currentIndex = 0;
          }
          this.currentQuran = this.listOfQuran[this.currentIndex];
          this.play(this.currentQuran);
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause: function() {
      this.player.pause();
      this.isPlaying = false;
    },
    next: function() {
      this.currentIndex++;
      this.currentIndex %= this.listOfQuran.length;
      this.currentQuran = this.listOfQuran[this.currentIndex];
      this.play(this.currentQuran);
    },
    prev: function() {
      this.currentIndex--;
      if (this.currentIndex < 0) {
        this.currentIndex = this.listOfQuran.length - 1;
      }
      this.currentQuran = this.listOfQuran[this.currentIndex];
      this.play(this.currentQuran);
    }
  },
  created: function() {
    this.currentQuran = this.listOfQuran[this.currentIndex];
    this.player.src = this.currentQuran.src;
  }
};
</script>


<style scoped>
@import "./../css/Home.css";
</style>