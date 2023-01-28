<template>
    <div class="tableft__container">
        <span class="bar_icon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.2.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M0 96C0 78.3 14.3 64 32 64H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 128 0 113.7 0 96zM64 256c0-17.7 14.3-32 32-32H480c17.7 0 32 14.3 32 32s-14.3 32-32 32H96c-17.7 0-32-14.3-32-32zM448 416c0 17.7-14.3 32-32 32H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H416c17.7 0 32 14.3 32 32z"/></svg>
            <h2> MUSIC PAGE</h2>
        </span>
        <ul class="tableft__content">
                <li>Cá Nhân</li>
                <li>Khám Phá</li>
                <li>Bảng Xếp Hạng</li>
                <li>Radio</li>
                <li>Nhạc Mới</li>
                <li>Thể Loại</li>
                <li>Top 100</li>
            </ul>
    </div>
</template>
<script>
export default {

}
</script>

<style scoped>
*{
    color: #ffff;
}
.tableft__container{
    width: 20%;
    height: 100vh;
}
.bar_icon{
    display: flex;
}
.bar_icon svg{
    width: 30px;
    margin-right: 12px;
    fill: #ffff;
}
.tableft__content{
    padding-left: 12px;
}
.tableft__content li{
    cursor: pointer;
    padding: 8px 12px 8px 12px;
    list-style-type: none;
    font-size: 18px;
    font-weight: 600;
    width: 180px;
}
.tableft__content li:hover{
    background: #85FFBD;
    background: -webkit-linear-gradient(to right, #85FFBD, rgba(224, 254, 251, 0.1)); 
    background: linear-gradient(to right, #85FFBD, rgba(224, 254, 251, 0.1)); 
    border-radius: 12px;
}
</style>