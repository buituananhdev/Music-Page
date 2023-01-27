<template>
    <div class="tableft__container">
        <h2>DANH SACH PHAT</h2>
        <ul class="list_songs" v-for="song in list_songs" :key="song.encodeId">
            <li class="song" @click="ChooseSong(song)">
                <img :src="song.thumbnailM" alt="">
                {{ song.title }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ["list_songs"],
    methods: {
        ChooseSong(song) {
            this.$emit("ChooseSong", song);
        }
    },
}
</script>

<style scoped>
img{
    width: 40px;
    margin-right: 12px;
    border-radius: 5px;
}
.tableft__container{
    width: 20%;
    height: 90vh;
    overflow: scroll;
    margin-left: 24px;
}
.tableft__container::-webkit-scrollbar {
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
    background: #85FFBD;
    background: -webkit-linear-gradient(to right, #85FFBD, #FFFB7D); 
    background: linear-gradient(to right, #85FFBD, #FFFB7D); 
    border-radius: 5px;
}
</style>