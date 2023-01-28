<template>
    <div class="tabright__container">
        <h3>DANH SÁCH PHÁT</h3>
        <ul class="list_songs" v-for="song in list_songs" :key="song.encodeId">
            <li :class="song.encodeId" class="song" @click="ChooseSong(song)">
                <span class="index_song">{{ ++index_song }}</span>
                <img :src="song.thumbnailM" alt="">
                <span class="infor_song">
                    {{ song.title }}
                <small class="artistsNames">{{ song.artistsNames }}</small>
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ["list_songs"],
    data(){
        return{
            index_song: -4040,
            current_song: null,
        }
    },  
    methods: {
        ChooseSong(song) {
            this.$emit("ChooseSong", song);
            document.querySelectorAll('.song').forEach((item) => {
                item.classList.remove('active');
            })
            document.querySelector('.' + song.encodeId).classList.add('active');
        }
    },
}
</script>

<style scoped>
.active{
    background: linear-gradient(to right, #dff6ea, #233329); 
    border-radius: 5px;
}

img{
    width: 40px;
    margin-right: 12px;
    border-radius: 5px;
}
.tabright__container{
    width: 100%;
    height: 90vh;
    overflow: scroll;
    margin-left: 24px;
}
.tabright__container::-webkit-scrollbar {
    display: none;
}
.list_songs{
    padding-left: 0;
}
.list_songs li{
    list-style-type: none;
    padding: 6px;
    font-weight: 500;
    cursor: pointer;
    display: flex;
    align-items: center;
}
.list_songs li:hover{
    background: linear-gradient(to right, #dff6ea, #233329); 
    border-radius: 5px;
}
.infor_song{
    display: flex;
    flex-direction: column;
}
.artistsNames{
    font-size: 11px;
    font-weight: 400;
}
.index_song{
    color: rgb(165, 164, 164);
    margin-right: 18px;
    margin-left: 10px;
    font-size: 16px;
    font-weight: 900;
}
</style>