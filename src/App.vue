<template>
  <div>
    <h1>Addicted</h1>
    <section class="player">
      <h3 class="title">Playing: {{ playing.title }}</h3>
      <button class="play" @click="stop">stop</button>
      <button class="play" v-if="isPlay" @click="play(songs[0])">Play</button>
      <button class="play" @click="next">Next</button>
    </section>
    <div class="playlist">
      <h2>In This</h2>
      <li v-for="song in songs" :key="song.src">
        {{ song.title }}
      </li>
    </div>
    <p>Built by <a href="https://github.com/sidhoh">Sidh</a> 🍉, with VueJS.</p>
   </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      isPlay: true,
      playing: {},
      songs: [
        {
          title: "Beck - Loser",
          source: require("./songs/Beck - Loser.mp3"),
        },
        {
          title: "Blind Melon - No Rain",
          source: require("./songs/Blind Melon - No Rain.mp3"),
        },
        {
          title: "Bush - Glycerine",
          source: require("./songs/Bush - Glycerine.mp3"),
        },
        {
          title: "Camila Cabello - Never Be The Same",
          source: require("./songs/Camila Cabello - Never Be The Same.mp3"),
        },
        {
          title: "Beck - Childish Gambino - This Is America",
          source: require("./songs/Childish Gambino - This Is America.mp3"),
        },
        {
          title: "Collective Soul - Shine",
          source: require("./songs/Collective Soul - Shine.mp3"),
        },
        {
          title: "Dishwalla - Counting Blue Cars",
          source: require("./songs/Dishwalla - Counting Blue Cars.mp3"),
        },
        {
          title: "Dishwalla - Counting Blue Cars",
          source: require("./songs/Dynoro & Gigi D'Agostino - In My Mind.mp3"),
        },
        {
          title: "Faith No More - Epic",
          source: require("./songs/Faith No More - Epic.mp3"),
        },
        {
          title: "Filter - Hey Man Nice Shot",
          source: require("./songs/Filter - Hey Man Nice Shot.mp3"),
        },
      ],
      index: 1,
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.source != "undefined") {
        this.playing = song;
        this.player.src = this.playing.source;
      }
      this.isPlay = false;
      this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }
          this.playing = this.songs[this.index];
          this.play(this.playing);
        }.bind(this)
      );
    },
    stop() {
      this.isPlay = true;
      this.player.pause();
      this.player.currentTime = 0;
      this.index = 1;
    },
    next() {
      let index = this.index++;
      this.playing = this.songs[index];
      this.play(this.playing);
    },
  },
};
</script>
