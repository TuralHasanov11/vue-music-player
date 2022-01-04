<template>
    <section id="music-section">
        

        <div id="blog" class="blog">
            <div class="container">
                <div class="row">
                    <div class="col-lg-4 offset-lg-4">
                    <div class="section-heading">
                        <h6>Playlist</h6>
                        <h4>Check <em>Songs</em></h4>
                        <div class="line-dec"></div>
                    </div>
                    </div>
                    <div class="col-lg-6 show-up mb-4">
                        <div class="blog-post">
                            
                            <div class="down-content">
                                <span class="category">{{ current.category }}</span>
                                <a href="#"><h4>{{ current.title }}</h4></a>
                                
                                <div class="music-container play" :class="{'play':isPlaying}" :style="{'box-shadow':'0 1.25em 1.25em 0 '+current.color_2}" id="music-container">

                                    <div class="music-info">
                                        
                                        <div class="time-duration">
                                            <span>{{ currTime }}</span>
                                            <span>{{ durTime }}</span>
                                        </div>
                                        <div @click="setProgress($event)" class="progress-container" id="progress-container">
                                            <div class="progress" id="progress" :style="{'width':progress, 'background-color':current.color_2?current.color_2:'#726ae3'}"></div>
                                        </div>
                                    </div>

                                    <div class="img-container">
                                        <img :src="current.cover" alt="music-cover" id="cover" />
                                    </div>

                                    <div class="navigation">
                                        <button id="prev" @click="prev" class="action-btn">
                                            <i class="fas fa-backward"></i>
                                        </button>
                                        <button id="play" class="action-btn action-btn-big">
                                            <i v-if="!isPlaying" @click="play()" class="fas fa-play"></i>
                                            <i v-else @click="pause" class="fas fa-pause"></i>
                                        </button>
                                        <button id="next" @click="next" class="action-btn">
                                            <i class="fas fa-forward"></i>
                                        </button>
                                    </div>

                                </div>

                                <span class="author"><img :src="current.artist_cover" alt=""><b>By: {{ current.artist }}</b></span>
                            </div>
                        </div>
                    </div>

                    <div class="col-lg-6">
                        <div class="blog-posts">
                            <div class="row">
                                <div  v-for="(song, key) in songs" :key="key" @click="play(song)" class="col-lg-12 song" :class="song.src == current.src ? 'song-playing' : ''">
                                    <div class="post-item">
                                        <div class="right-content d-flex align-items-center justify-content-between">
                                            <a class="mx-3" href="#"><h4>{{song.title}}</h4></a>
                                            <div>
                                              <span class="date mx-2">{{song.artist}}</span>
                                              <span class="category mx-2">{{song.category}}</span>
                                            </div>
                                            <!-- <p>Lorem ipsum dolor sit amet, cocteturi adipiscing eliterski.</p> -->
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
        </div> 
    </section>
</template>

<script>
export default {
  data() {
    return {
      current: {
        title: null,
        artist: null,
        src: null,
        cover: null,
      },
      songs: [
        {
          title: "Valhalla",
          artist: "Sarah Schachner, Jesper Kyd",
          category:'Other',
          artist_cover: require("@/assets/artist_images/summer.jpg"),
          src: require("@/assets/music/Valhalla.mp3"),
          cover: require("@/assets/music_images/summer.jpg"),
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(39, 146, 87)'

        },
        {
          title: "Attila",
          artist: "Total War Attila",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/Attila.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(255, 166, 0)'
        },
        {
          title: "Ezio's Family",
          artist: "Ubisoft",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/Ezio.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgba(247, 247, 247)',
          color_2:'rgb(255, 103, 77)'
        },
        {
          title: "The North Remembers",
          artist: "Ramin Djawadi",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/North_Remembers.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(25, 139, 214)'
        },
        {
          title: "Odyssey",
          artist: "Ubisoft",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/Odyssey.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(255, 71, 71)',
          color_2:'rgb(25, 139, 214)'
        },
        {
          title: "The Winter Has Come",
          artist: "Ramin Djawadi",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/Winter_Has_Come.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(172, 13, 13)'
        },
        {
          title: "Swadian Hall",
          artist: "Taleworlds",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/Swadian_Hall.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(241, 141, 74)',
          color_2:'rgb(165, 91, 42)'
        },
        {
          title: "Rohan Theme (LOTR)",
          artist: "LOTR",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/Lotr.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(41, 16, 1)',
          color_2:'rgb(39, 146, 87)'
        },
        {
          title: "Town Song",
          artist: "Taleworlds",
          category:'Soundtrack',
          artist_cover: require("@/assets/artist_images/hey.jpg"),
          src: require("@/assets/music/M&B.mp3"),
          cover: require("@/assets/music_images/hey.jpg"),
          color_1:'rgb(241, 141, 74)',
          color_2:'rgb(165, 91, 42)'
        },
       
      ],
      index: 0,

      player: null,
      isPlaying: false,
      progress: null,

      sec: null,
      secD: null,
      min: null,
      minD: null,
      currTime: '00:00',
      durTime: '00:00',
    };
  },

  created() {
    this.player = new Audio()
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    document.body.style.background = `linear-gradient(0deg, ${this.current.color_1} 23.8%, ${this.current.color_2} 92%)`; 

  },
  

  methods: {

    reset(){
      this.progress = null

      this.sec= null
      this.secD= null
      this.min= null
      this.minD= null
      this.currTime= '00:00'
      this.durTime= '00:00'
    },


    play(song = null) {

      if (song && song.src != "") {
        this.reset()

        this.current = song;

        this.player.src = this.current.src;
        

        document.body.style.background = `linear-gradient(0deg, ${song.color_1} 23.8%, ${song.color_2} 92%)`; 
      }

      this.player.play();

      this.player.addEventListener(
        "ended",
        function () {
          this.next();
        }.bind(this)
      );

      this.player.addEventListener("timeupdate", function () {
          this.updateProgress();
          this.DurTime();
        }.bind(this)
      );

      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];

      this.play(this.current);
    },

    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];

      this.play(this.current);
    },

    updateProgress() {
        this.progress = `${(this.player.currentTime / this.player.duration) * 100}%`
    },

    setProgress(event) {
     
      this.player.currentTime = (event.offsetX / event.currentTarget.clientWidth) * this.player.duration;
    },

    //get duration & currentTime for Time of song
    DurTime() {

      // define minutes currentTime
      this.min = this.player.currentTime == null ? 0 : Math.floor(this.player.currentTime / 60);
      this.min = this.min < 10 ? "0" + this.min : this.min;

      // define seconds this.player.currentTime
      this.getSec(this.player.currentTime);

      // change currentTime DOM
      this.currTime = this.min + ":" + this.sec;

      // define minutes duration
      this.minD = isNaN(this.player.duration) === true ? "0" : Math.floor(this.player.duration / 60);
      this.minD = this.minD < 10 ? "0" + this.minD : this.minD;

      // define seconds this.player.duration
      this.getSecD(this.player.duration, this.player.duration);

      // change duration DOM
      this.durTime = this.minD + ":" + this.secD;
    },

    getSec(x) {
      if (Math.floor(x) >= 60) {
        for (var i = 1; i <= 60; i++) {
          if (Math.floor(x) >= 60 * i && Math.floor(x) < 60 * (i + 1)) {
            this.sec = Math.floor(x) - 60 * i;
            this.sec = this.sec < 10 ? "0" + this.sec : this.sec;
          }
        }
      } else {
        this.sec = Math.floor(x);
        this.sec = this.sec < 10 ? "0" + this.sec : this.sec;
      }
    },

    getSecD(x) {
      if (Math.floor(x) >= 60) {
        for (var i = 1; i <= 60; i++) {
          if (Math.floor(x) >= 60 * i && Math.floor(x) < 60 * (i + 1)) {
            this.secD = Math.floor(x) - 60 * i;
            this.secD = this.secD < 10 ? "0" + this.secD : this.secD;
          }
        }
      } else {
        this.secD = isNaN(this.duration) === true ? "0" : Math.floor(x);
        this.secD = this.secD < 10 ? "0" + this.secD : this.secD;
      }
    },
  },
};
</script>


<style>
body {
  animation: gradient 5 ease infinite !important;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>