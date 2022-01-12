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
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fvalhalla-artist.jpg?alt=media&token=a4aa17d2-6e98-4e1e-a77c-e09105d6e0fe',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FValhalla.mp3?alt=media&token=cce74c3e-e429-4b01-ba27-1bf7702e8a78',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fvalhalla.jpg?alt=media&token=90b93c56-6df1-4549-a974-56bd09a70a7f',
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(39, 146, 87)'
        },
        {
          title: "Attila",
          artist: "Total War Attila",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fattila-artist.png?alt=media&token=84d199ba-ef9b-463f-b9e7-0cffa097ba02',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FAttila.mp3?alt=media&token=bf2f8fc2-e4a4-4ddd-9b53-a12f499be001',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fattila.jpg?alt=media&token=07bcc733-6c63-45b9-a6a6-65d8cbe45740',
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(255, 166, 0)'
        },
        {
          title: "Ezio's Family",
          artist: "Ubisoft",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fezio-artist.jpg?alt=media&token=ae5c8d92-6c9e-4f5d-ae9a-5ca0727d93ce',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FEzio.mp3?alt=media&token=05a0817b-9089-4f37-8e31-c83af64e6491',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fezio.jpg?alt=media&token=8c40de6e-e621-4095-897d-0ab34a416d6c',
          color_1:'rgba(247, 247, 247)',
          color_2:'rgb(255, 103, 77)'
        },
        {
          title: "The North Remembers",
          artist: "Ramin Djawadi",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fnorth-remembers-artist.jpg?alt=media&token=c6b6c4e0-120f-4c97-a0f1-68a4f2d7a917',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FNorth_Remembers.mp3?alt=media&token=e6cdefba-f63e-4963-8dbd-811ae3f3a535',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fnorth_remembers.jpg?alt=media&token=39554c95-97bc-40ad-a11b-32eb397d985a',
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(25, 139, 214)'
        },
        {
          title: "Odyssey",
          artist: "Ubisoft",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fezio-artist.jpg?alt=media&token=ae5c8d92-6c9e-4f5d-ae9a-5ca0727d93ce',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FOdyssey.mp3?alt=media&token=d8f0d1d7-d149-4618-92f2-626e6913b143',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fodyssey.jpg?alt=media&token=487a5e6e-43c3-4b97-8752-c3a71b66d073',
          color_1:'rgb(255, 71, 71)',
          color_2:'rgb(25, 139, 214)'
        },
        {
          title: "The Winter Has Come",
          artist: "Ramin Djawadi",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fnorth-remembers-artist.jpg?alt=media&token=c6b6c4e0-120f-4c97-a0f1-68a4f2d7a917',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FWinter_Has_Come.mp3?alt=media&token=4520a6b1-00b4-4bfc-bb29-a71ff4165518',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fwinter-has-come.jpg?alt=media&token=05d2684e-bf02-4685-a5c7-3a146c61d5d2',
          color_1:'rgb(10, 10, 10)',
          color_2:'rgb(172, 13, 13)'
        },
        {
          title: "Swadian Hall",
          artist: "Taleworlds",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Ftaleworlds.png?alt=media&token=f60a70c9-e456-4021-8880-f8aef8fab7bf',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FSwadian_Hall.mp3?alt=media&token=23b1d9da-9c61-4bb6-b5e6-086236a28fd1',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Fswadian-hall.jpg?alt=media&token=390864d9-5b93-4674-8478-eaf6f04f0f8e',
          color_1:'rgb(241, 141, 74)',
          color_2:'rgb(165, 91, 42)'
        },
        {
          title: "Rohan Theme (LOTR)",
          artist: "LOTR",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Flotr.jpg?alt=media&token=252a4450-e6f7-4aa0-82d6-1d73f80e7300',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FLotr.mp3?alt=media&token=5244afbb-2ffb-4808-80ec-a0868a168d45',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Frohan.jpg?alt=media&token=2fd7314f-ac27-48c4-8812-8d82deb32ca4',
          color_1:'rgb(41, 16, 1)',
          color_2:'rgb(39, 146, 87)'
        },
        {
          title: "Town Song",
          artist: "Taleworlds",
          category:'Soundtrack',
          artist_cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2Ftaleworlds.png?alt=media&token=f60a70c9-e456-4021-8880-f8aef8fab7bf',
          src: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/songs%2FM%26B.mp3?alt=media&token=236e4005-d65a-41e7-b48e-de607a61e372',
          cover: 'https://firebasestorage.googleapis.com/v0/b/vuemusicplayer-ab294.appspot.com/o/images%2FM%26B-Town.jpg?alt=media&token=9f2695fe-f5cd-405f-8571-249e52d37acf',
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