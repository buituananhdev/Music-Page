<template>
  <div class="app__container">
    <div id="app">
      <TabLeft></TabLeft>
      <div class="main__content">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
          <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
        </svg>
        <input class="search" type="text" placeholder="Bạn muốn nghe gì?" v-model="search_value" @keyup="search_song">
        <svg v-if="search_value!=''" @click="search_value=''" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="circle-xmark" class="svg-inline--fa fa-circle-xmark " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M0 256C0 114.6 114.6 0 256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C114.6 512 0 397.4 0 256zM175 208.1L222.1 255.1L175 303C165.7 312.4 165.7 327.6 175 336.1C184.4 346.3 199.6 346.3 208.1 336.1L255.1 289.9L303 336.1C312.4 346.3 327.6 346.3 336.1 336.1C346.3 327.6 346.3 312.4 336.1 303L289.9 255.1L336.1 208.1C346.3 199.6 346.3 184.4 336.1 175C327.6 165.7 312.4 165.7 303 175L255.1 222.1L208.1 175C199.6 165.7 184.4 165.7 175 175C165.7 184.4 165.7 199.6 175 208.1V208.1z"></path></svg>
        <div class="result__search" v-if="search_value != ''">
          <small>Gợi ý kết quả</small>
          <ul class="list_songs_search" v-for="song of list_songs_search" :key="song.encodeId">
            <li class="song_search" @click="ChooseSong(song)">
                <img class="img_song_search" :src="song.thumbnailM" alt="">
                <span class="infor_song_search">
                    {{ song.title }} 
                <small class="artistsNames">{{ song.artistsNames }}</small>
                </span>
                
            </li>
        </ul>
        </div>
        <div class="infor_song">
          <div class="img_container">
            <img class="img_song" :src="thumbnailM" alt="">
            <div class="image__overlay">
              <img class="wave_gif" src="./assets/giphy.gif" alt="">
            </div>
          </div>
          <p class="name_song">{{ name_song }}</p>
          <p class="artist_Name">{{ artist_Name }} • {{ new Date(releaseDate).toLocaleDateString('en-US', optionsTime) }}</p>
          <div class="action_btn">
              <div class="action__song">
                <svg class="heart__icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.2.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M244 84L255.1 96L267.1 84.02C300.6 51.37 347 36.51 392.6 44.1C461.5 55.58 512 115.2 512 185.1V190.9C512 232.4 494.8 272.1 464.4 300.4L283.7 469.1C276.2 476.1 266.3 480 256 480C245.7 480 235.8 476.1 228.3 469.1L47.59 300.4C17.23 272.1 0 232.4 0 190.9V185.1C0 115.2 50.52 55.58 119.4 44.1C164.1 36.51 211.4 51.37 244 84C243.1 84 244 84.01 244 84L244 84zM255.1 163.9L210.1 117.1C188.4 96.28 157.6 86.4 127.3 91.44C81.55 99.07 48 138.7 48 185.1V190.9C48 219.1 59.71 246.1 80.34 265.3L256 429.3L431.7 265.3C452.3 246.1 464 219.1 464 190.9V185.1C464 138.7 430.4 99.07 384.7 91.44C354.4 86.4 323.6 96.28 301.9 117.1L255.1 163.9z"/></svg>
                <div class="tooltiptext">
                  Thêm vào yêu thích
                </div>
              </div>
              
              <div class="action__song">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.2.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M120 256c0 30.9-25.1 56-56 56s-56-25.1-56-56s25.1-56 56-56s56 25.1 56 56zm160 0c0 30.9-25.1 56-56 56s-56-25.1-56-56s25.1-56 56-56s56 25.1 56 56zm104 56c-30.9 0-56-25.1-56-56s25.1-56 56-56s56 25.1 56 56s-25.1 56-56 56z"/></svg>
                <span class="tooltiptext">
                  Khác
                </span>
              </div>
          </div>
          
        </div>
        <div class="other_song">
          <TabRight class="" v-bind:list_songs="list_songs" @ChooseSong="ChooseSong"></TabRight>
        </div>
      </div>
    </div>
    <PlayerBar :url_song="url_song" :thumbnailM="thumbnailM" :name_song="name_song" :artist_Name="artist_Name"></PlayerBar>
  </div>
</template>

<script>
import TabLeft from './components/TabLeft.vue';
import TabRight from './components/TabRight.vue';
import PlayerBar from './components/PlayerBar.vue';
import axios from 'axios';
export default{
  components: {
    TabLeft,
    TabRight,
    PlayerBar,
  },
  data(){
    return{
      list_songs: [],
      list_songs_search: [],
      search_value: "",
      name_song: "Quả Phụ Tướng",
      artist_Name: "Dunghoangpham",
      releaseDate: 0,
      thumbnailM: "https://photo-resize-zmp3.zmdcdn.me/w240_r1x1_jpeg/cover/8/6/7/d/867dea78919c4ad9e000d1385c9042ab.jpg",
      url_song: "https://mp3-s1-zmp3.zmdcdn.me/d3d17f522912c04c9903/487704677693875669?authen=exp=1674977880~acl=/d3d17f522912c04c9903/*~hmac=fd647fabacc295365b0082a4cc2fd8bf&fs=MTY3NDgwNTA4MDIxMXx3ZWJWNnwwfDE0LjE5MS4yMjQdUngMjEz",
    }
  },
  mounted () {
    document.body.classList.add('body__class');
    this.fetch_Home();
  },
  methods: {
    async fetch_Home() {
      try {
        await axios.get(`https://zing-mp3-api.vercel.app/api/chart/home`).then(res => {
          let tmp = res.data;
          this.list_songs = tmp.data.weekChart.vn.items;
          console.log(this.list_songs);
          this.current_song = this.list_songs[0];
          console.log(this.current_song);
        });
      } catch(error){
        console.log(error)
      }
    },
    async ChooseSong(song){
      
      try {
        await axios.get(`https://zing-mp3-api.vercel.app/api/song/${song.encodeId}`).then(res => {
          this.url_song = Object.values(res["data"].data)[0];
          this.thumbnailM = song.thumbnailM;
          this.name_song = song.title;
          this.artist_Name = song.artistsNames;
          this.releaseDate = song.releaseDate;
        });
      } catch(error){
        console.log(error)
      }
    },
    search_song(){
      this.list_songs_search = [];
            this.list_songs.filter((item) => {
                if (item.title.toUpperCase().indexOf(this.search_value.toUpperCase()) > -1) {
                    this.list_songs_search.push(item);
                }
            })
    },
  },
}
</script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
  .body__class::-webkit-scrollbar{
    display: none;
  }
  .body__class{
    
    background: #85FFBD;
    background: linear-gradient(to right, #233329, #63D471);
  }
  *{
    font-family: 'Montserrat', sans-serif;
  }
</style>
<style scoped>
.fa-circle-xmark{
  width: 20px;
  position: absolute;
  right: 70px;
  top: 34px;
  color: rgb(192,192,192);
  cursor: pointer;
}
.action__song .tooltiptext {
  font-size: 12px;
  width: 120px;
  visibility: hidden;
  background-color: rgba(0, 0, 0, 0.3);
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  /* Position the tooltip */
  position: absolute;
  z-index: 10;
  top: -30px;
}
.action__song:hover .tooltiptext {
  visibility: visible;
}
.action_btn{
  margin-top: 24px;
  display: flex;
}
.action__song{
  position: relative;
  width: 40px;
  height: 40px;
  background-color: #63D471;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  margin-left: 55px;
}
.action__song svg{
  width: 18px;
  fill: #233329;
}
.bi-search{
  position: relative;
  z-index: 3;
  top: -12px;
  right: -15px;
  color: rgb(0 0 0);
}
.img_song_search{
  width: 40px;
  margin-right: 12px;
  border-radius: 5px;
}
.result__search{
  position: absolute;
  z-index: 1;
  width: 32%;
  height: 80%;
  background-color: #f1f9f5;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  margin-top: 24px;
  border-radius: 5px;
  padding: 12px;
  overflow: scroll;
  color: #233329;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
}
.result__search::-webkit-scrollbar{
  display: none;
}
.list_songs_search{
    padding-left: 0;
}
.list_songs_search li{
    list-style-type: none;
    padding: 6px;
    font-weight: 500;
    cursor: pointer;
    display: flex;
    align-items: center;
}
.list_songs_search li:hover{
    background: #85FFBD;
    background: -webkit-linear-gradient(to right, #85FFBD, #fffca5); 
    background: linear-gradient(to right, #85FFBD, #fffca5); 
    border-radius: 5px;
}
.infor_song_search{
    display: flex;
    flex-direction: column;
}
.artistsNames{
    font-size: 11px;
    font-weight: 400;
}
.app__container{ 
  padding: 12px;
  
}
#app{
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
}
.main__content{
  padding: 48px;
  width: 75%;
  height: 68vh;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  border-radius: 24px;
  position: relative;
  display: flex;
  overflow: hidden;
  background-color: #233329;
  color: #ffff;

}
.search{
  position: absolute;
  top: 25px;
  width: 80%;
  font-size: 15px;
  padding: 10px 50px 10px 42px;
  border-radius: 24px;
  border: none;
  background-color: #f1f9f5;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 0px 5px 0px, rgba(0, 0, 0, 0.1) 0px 0px 1px 0px;
}
.search:focus{
  outline-width: 0;
}
.image__overlay{
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  border-radius: 24px;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  transform: scale(0);
  transition: all 0.2s ease 0s;
}
.img_song{
  max-width: 100%;
  width: 260px;
  height: 260px;
  border-radius: 24px;
  transition: all 0.3s ease 0s;
}
.wave_gif{
  width: 90px;
  opacity: .7;
}
.img_container{
  position: relative;
  width: 260px;
  height: 260px;
  overflow: hidden;
  border-radius: 24px;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}
.img_container:hover .image__overlay{
  transform: scale(1);
}
.img_container:hover .img_song{
  transform: scale(1.1);
}

@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}
.infor_song{
  text-align: center;
  flex: 0.4;
}
.other_song{
  flex: 1.6;
  padding-bottom: 48px;
  overflow: hidden;
  margin-left: 48px;
}
.infor_song,.other_song{
  margin-top: 32px;
  padding: 12px;
}
.name_song{
  margin-bottom: 6px;
  font-size: 30px;
  font-weight: 700;
}
.artist_Name{
  font-size: 14px;
  font-weight: 400;
}
</style>