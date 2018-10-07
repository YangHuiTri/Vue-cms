<template>
    <div class="goodsinfo-container">
        
        <!-- 商品轮播图区域 -->
        <div class="mui-card">
            <div class="mui-card-content">
                <div class="mui-card-content-inner">
                    <swiper :lunbotuList="lunbotu" :isfull="false"></swiper>
                </div>
            </div>
        </div>




        <!-- 商品购买区域 -->
        <div class="mui-card">
            <div class="mui-card-header">商品的名称标题</div>
            <div class="mui-card-content">
                <div class="mui-card-content-inner">
                    <p class="price">
                        市场价：<del>￥2399</del>&nbsp;&nbsp;销售价：<span class="now_price">￥2199</span>
                    </p>
                    <p>购买数量：<numbox></numbox></p>
                    <p>
                        <mt-button type="primary" size="small">立即购买</mt-button>
                        <mt-button type="danger" size="small">加入购物车</mt-button>
                    </p>
                </div>
            </div>
        </div>





        <!-- 商品参数区域 -->
        <div class="mui-card">
            <div class="mui-card-header">页眉</div>
            <div class="mui-card-content">
                <div class="mui-card-content-inner">
                    包含页眉页脚的卡片，页眉常用来显示面板标题，页脚用来显示额外信息或支持的操作（比如点赞、评论等）
                </div>
            </div>
            <div class="mui-card-footer">页脚</div>
        </div>

    </div>

    <!-- 分析：为什么商品评论上面的轮播图那么丑 -->
    <!-- 1.首页中的轮播图图片都使用了100%的宽度 -->
    <!-- 2.在商品详情页面中，轮播图的图片如果也使用宽高为100%的话，页面不好看 -->
    <!-- 3.商品详情页面中的轮播图，期望高度是100%，但是宽度为自适应 -->
    <!-- 4.经过分析，得到问题的原因：首页中的轮播图和详情中的轮播图，分歧点是宽度到底是100%还是自适应 -->
    <!-- 5.既然这两个轮播图其他方面都是没有冲突的，只是宽度有分歧，那么我们可以定义一个属性，让使用轮播图的调用者收订指定是否为100%宽度 -->
</template>

<script>
//导入轮播图组件
import swiper from '../subcomponents/swiper.vue'
//导入数字选择框组件
import numbox from '../subcomponents/goodsinfo_numbox.vue'
    export default{
        data(){
            return{
                id: this.$route.params.id,  //将路由参数对象中的id挂载到data，方便后期调用
                lunbotu: []     //轮播图的数据
            }
        },
        created() {
            this.getLunbotu();
        },
        methods:{
            getLunbotu(){
                this.$http.get("api/getthumimages/" + this.id).then(result => {
                    if(result.body.status === 0){
                        //先循环轮播图数组的每一项，为item添加img属性，因为轮播图组件中只认识item.img，不认识item.src
                        result.body.message.forEach(item=>{
                            item.img = item.src;
                        });
                        this.lunbotu = result.body.message;
                    }
                })
            }
        },
        components: {
            swiper,
            numbox
        }
    }
</script>

<style lang="scss" scoped>
.goodsinfo-container{
    background-color: #eee;
    overflow: hidden;

    .now_price{
        color: red;
        font-size: 16px;
        font-weight: bold;
    }
}
</style>

