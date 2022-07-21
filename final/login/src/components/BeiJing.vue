<template>
    <div class="kk">
            <img src="@/assets/dt.jpg" alt="" class="img">
    </div>
</template>

<script>

</script>

<style>
    .kk{
        height: 100%;
        width: 100%;
        /*把背景图片放大到适合元素容器的尺寸，图片比例不变*/
        background-size:cover;
        position:absolute;
        left:0;
        top:6%;
    }
    .img{
        width: 100%;
        height:80%;
         /*元素的位置相对于浏览器窗口是固定位置*/
        left: 0;
        top: 0;
    }
</style>