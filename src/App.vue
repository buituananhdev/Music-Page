<template>
  <div class="app__container">
    <div id="app">
      <TabLeft></TabLeft>
      <div class="main__content">
        <input class="search" type="text" placeholder="Search here">
        <div class="infor_song">
          <div class="img_container">
            <img class="img_song" :src="thumbnailM" alt="">
          </div>
          <p class="name_song">{{ name_song }}</p>
          <p class="artist_Name">{{ artist_Name }}</p>
        </div>
        <div class="other_song">
          aaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
        </div>
      </div>
      <TabRight class="" v-bind:list_songs="list_songs" @ChooseSong="ChooseSong"></TabRight>
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
      name_song: "Quả Phụ Tướng",
      artist_Name: "Dunghoangpham",
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
        });
      } catch(error){
        console.log(error)
      }
    }
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
    background: linear-gradient(to right, #b1fdd5, #fffca5);
  }
  *{
    font-family: 'Montserrat', sans-serif;
  }
</style>
<style scoped>
.app__container{ 
  padding: 24px;
  margin-left: 48px;
  margin-right: 48px;
}
#app{
  margin: 12px auto;
  display: flex;
}
.main__content{
  padding: 48px;
  width: 60%;
  height: 85vh;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  border-radius: 24px;
  position: relative;
  display: flex;
}
.search{
  position: absolute;
  top: 25px;
  width: 85%;
  font-size: 15px;
  padding: 8px 12px 8px 18px;
  border-radius: 24px;
  border: none;
  background-color: #f1f9f5;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 0px 5px 0px, rgba(0, 0, 0, 0.1) 0px 0px 1px 0px;
}
.search:focus{
  outline-width: 0;
}
.img_container{
  width: 280px;
  height: 280px;
  overflow: hidden;
  border-radius: 12px;
}
.img_song{
  max-width: 100%;
  width: 280px;
  height: 280px;
  transition: 0.4s;
}
.img_song:hover{
  transform: scale(1.1);
}
.infor_song{
  margin: 0 auto;
}
.infor_song,.other_song{
  margin-top: 32px;
  padding: 12px;
  flex: 1;
}
.name_song{
  font-size: 22px;
  font-weight: 600;
}
</style>