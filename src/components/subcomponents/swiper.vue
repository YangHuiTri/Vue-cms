<template>
    <div>
        <mt-swipe :auto="4000">
            <!-- 在组建中，使用v-for循环的话，一定要使用key -->
            <!-- 将来，谁使用此轮播图组件，谁为我们传递lunbotuList -->
            <!-- 此时，lunbotuList应该是父组件向子组件传值来设置 -->
        <mt-swipe-item v-for="item in lunbotuList" :key="item.url">
            <img :src="item.img" alt="" :class="{'full': isfull}">
        </mt-swipe-item>
        </mt-swipe>
    </div>
</template>

<script>
export default{
    props: ["lunbotuList", "isfull"]
}
</script>

<style lang="scss" scoped>
.mint-swipe{
    height: 200px;

    .mint-swipe-item{
        text-align: center;
        
        img{
            width: 100%;
            height: 100%;
        }
    }
}

.full{
    width: 100%;
}
</style>

