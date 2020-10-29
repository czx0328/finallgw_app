<template>
  <div class="home">
    <!-- 头部图片 -->
    <header class="header">
      <!-- <img src="../../assets/home.jpg" alt=""> -->
      <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="item in imagesbox" :key="item.id">
          <img :src="item.idView" class="image" size="100% 100%">
      </van-swipe-item>
      </van-swipe>
    </header>
    <!-- 内容区域 -->
    <div>
      <!-- 分类 6个-->
      <van-grid :column-num="3">
        <van-grid-item
          v-for="value in categories"
          :key="value.id"
          :icon="value.icon"
          :text="value.name"
        />
      </van-grid>
      <!-- 产品 n个-->
      <briup-product-item 
        @click="toBuyHandler(p)"
        v-for="p in products"
        :key="p.id" 
        :data="p">
      </briup-product-item>
      <!-- /产品 -->
    </div>
   
  </div>
</template>

<script>
import {get,post} from '../../http/axios';
export default {
  data(){
    return {
      categories:[],
      products:[],
       imagesbox:[{id:0,idView:"https://gdp.alicdn.com/imgextra/i3/917264765/O1CN01NPvSQf1l4PnI9qI57_!!917264765.jpg"},   
           {id:1,idView:"https://gdp.alicdn.com/imgextra/i2/917264765/O1CN010Wutft1l4Ps32BuxP_!!917264765.jpg"},

          {id:2,idView:"https://uxresources.baozun.com/prod/88000060/20201025/218A6D74A5E43C687CCA3C47E19552FA.jpg"}],
           active: 0
    }
  },
  created(){
    // 查询栏目信息
    this.loadCategories();
    // 查询产品
    this.loadProducts();
  },
  methods:{
    toBuyHandler(p){
      // 跳转到订单确认页面，并且携带数据p
      this.$router.push({
        path:"/manager/order_confirm",
        query:p
      })
    },
    // 加载栏目信息
    loadCategories(){
      let url = "/category/findAll";
      get(url).then((response)=>{
        // 将查询结果，数组中的前6个元素获取到
        this.categories = response.data.slice(0,6);
      })
    },
    // 加载产品信息
    loadProducts(){
      let url = "/product/query"
      let params = { page:0, pageSize:100 }
      post(url,params).then((response)=>{
        this.products = response.data.list;
      })
    }
  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 188px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
/* .el-carousel__item h3 {
    color: #475669;
    font-size: 18px;
    opacity: 0.75;
    line-height: 300px;
    margin: 0;
  }
  
.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n+1) {
  background-color: #d3dce6;
} */
.image{
  height: 188px;
}

</style>