<template>
  <div id="app">
      <header>
          <h1>My Music Playlist</h1>
      </header>
      <main>
          <section class="player">
              <h2 class="song-title">{{current.title}} - <span>{{ current.artist }}</span> </h2>
              <div class="controls">
                  <button class="prev" @click="prev">Prev</button>
                  <button class="play" v-if="!isPlaying" @click="play">Play</button>
                  <button class="pause" v-else @click="pause">Pause</button>
                  <button class="next" @click="next">Next</button>
              </div>
          </section>
          <section class="playlist">
              <h3>The Playlist</h3>
              <button v-for="song of songs" :key="song.src" @click="play(song) " :class="song.src == current.src ? 'song playing' : 'song' ">
                {{song.title}} - {{song.artist}}
              </button>
          </section>
      </main>
  </div>
</template>

<script>
    export default{

    data(){
      return{
        current:{},
        index: 0,
        isPlaying:false,
        songs:[
          {
            title:'Ghost Town',
            artist:'Adam Lambert',
            src:require('./assets/adam_lambert-ghost_town.mp3')
          },
           {
            title:'Mr Kitty',
            artist:'After Dark',
            src:require('./assets/Mr.Kitty - After Dark.mp3')
          },
           {
            title:'Mr Kitty',
            artist:'Hold me down',
            src:require('./assets/Mr. Kitty - Hold Me Down.mp3')
          },
           {
            title:'Trevor Something',
            artist:'Summer Love',
            src:require('./assets/Trevor Something - Summer Love (radio.lol).mp3')
          },
        ],
        player: new Audio()
      }
    },
   
    methods:{
      play(song){
        if(typeof song.src != 'undefined'){
            this.current = song;

            this.player.src = this.current.src
        }

        this.player.play()
        this.isPlaying = true
      },

      pause(){
        this.player.pause();
        this.isPlaying = false;
      },
      next(){
        this.index++;
        if(this.index > this.songs.length){
           this.index = 0;
        }
        this.current = this.songs[this.index]
        this.play(this.current)
      },
      prev(){
        this.index--;
        if(this.index < 0){
          this.index  = this.songs.length - 1;
        }
        this.current = this.songs[this.index]
        this.play(this.current)
      }
    },
     created(){
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
      // this.player.play()
    },
  }
</script>



<style>
    *{

      transition: 0.5s;
      margin: 0;
      padding: 0;
      box-sizing: border-box;

    }


    body{
      font-family: sans-serif;
    }

    

    header{
      display:flex;
      justify-content: center;
      padding: 15px;
      background: #212121;
      color: white;
      text-align: center;
    }
    main{
      width: 80%;
      margin: auto;
      padding: 25px;
    }

    .song-title{
      color: #212121;
      font-size: 32px;
      font-weight: 700;
      text-transform: uppercase;
      text-align: center;
    }

    .song-title span{
      font-weight: 400;
      font-style: italic;

    }
    .controls{
      display: flex;
      justify-content: center;
      padding: 30px 15px;
      align-items: center;
    }

    button{
      appearance: none;
      border:0;
      background: none;
      outline: 0;
      cursor: pointer;
    }
  
    button:hover{
      opacity: 0.8;
    }
    .play{
      font-size: 20px;
      font-weight: 700;
      padding: 15px 25px;
      margin: 0 15px;
      border-radius: 8px;
      color: #fff;
      background: #cc2e5d;
    }
    .pause{
      font-size: 20px;
      font-weight: 700;
      padding: 15px 25px;
      margin: 0 15px;
      border-radius: 8px;
      color: #fff;
      background: #cc2e5d;
    }
    .next , .prev{
      font-size: 16px;
      font-weight: 700;
      padding: 10px 20px;
      margin: 0 15px;
      border-radius:6px;
      color: #fff;
      background: #ff5858;
    }

    .playlist{
      padding: 0 30px;

    }

    .playlist h3{
      color: #212121;
      font-size: 28px;
      font-weight: 400;
      margin-bottom: 30px;
      text-align: center;

    }


    .playlist .song{
        display: block;
        width: 100%;
        padding: 15px;
        font-size: 20px;
        font-weight: 700;
        cursor: pointer;
    }
    .playlist .song:hover{
      color: #ff5858;
    }
    .playlist .song.playing{
      color: white;
      background:linear-gradient(to right , #cc2e5d , #ff5858);
    }
</style>