<template>
  <briup-fulllayout title="订单确认">
          <van-divider dashed><span class="van-cell-text">品牌折扣店</span>
          <van-tag class="goods-tag" type="danger">官方</van-tag></van-divider>
          <van-cell is-link @click="showPopup"><van-icon name="underway-o" size="large"/>&nbsp;折扣倒计时</van-cell>
          <van-popup v-model="show"><van-icon name="underway-o" size="large"/><br><br><br><van-count-down millisecond :time="time" format="HH:mm:ss:SS" style="height:100px;font-size:50px" /></van-popup>
          
    <van-tag plain type="primary" size="large" class="address"><van-icon name="location-o" />收货地址:</van-tag>
    <van-dropdown-menu>
      <van-dropdown-item v-model="addressId" :options="options" />
    </van-dropdown-menu>
    <van-panel title="订单详情" desc="这是您的订单信息" status="待确认">
      <div style="padding:0 2em">
     <p> <van-icon name="bag-o" />商品名称：{{$route.query.name}}</p>
      <van-divider />
      <p><van-icon name="orders-o" />商品简介：{{$route.query.description}}</p>
      <van-divider />
      <p><van-icon name="label-o" />所属品牌：{{$route.query.status}}</p>
      <van-divider />
      <p><van-icon name="balance-o" />商品价格：{{$route.query.price}}</p>
      <van-divider />
      <p><van-icon name="smile-o" />购买数量：1</p>
      <van-divider />
      <p><van-icon name="gold-coin-o" />金额小计：{{$route.query.price * 1}}</p>
      <van-divider />
    </div>
        </van-panel>
    <div style="position:fixed;bottom:0;width:100%;">
      <!-- <van-button @click="submitHandler" block type="primary">提交订单</van-button> -->
    <van-goods-action>
  <van-goods-action-icon icon="chat-o" text="客服" @click="onClickIcon" />
  <van-goods-action-icon icon="shop-o" text="店铺" @click="onClickstore" />
  <van-goods-action-button
    type="danger"
    text="提交订单"
    @click="submitHandler"
  />
</van-goods-action>
    </div>
  </briup-fulllayout>
</template>
<script>
import { mapState } from 'vuex'
import {get,post_obj_array} from '../../../http/axios'
export default {
  data(){
    return {
      addressId:0,    // 服务地址id
      addresses:[],
      orderLines:[],
      time: 30 * 60 * 60 * 1000,
      show: false,
    }
  },
  created(){
    // 在页面加载的时候查询地址信息
    this.loadAddress();
    // 初始化订单项（将我们购买的产品放入到购物车）
    let orderLine = {
      number:1,
      price:this.$route.query.price,
      productId:this.$route.query.id
    };
    this.orderLines.push(orderLine);
  },
  computed:{
    // 映射info信息
    ...mapState("user",["info"]),
    // [{id:1,province:'山西省',city:"晋中市"},{id:1,province:'江苏省',city:"昆山市"}] =》 [{text:"山西省晋中市",value:1}]
    options:function(){
      // 将addresses的数据计算为一个新的数组返回
      return this.addresses.map(item=>{
        return {
          text:item.province+" "+item.city+" "+item.area+" "+item.address,
          value:item.id
        }
      })
    }
  },
  methods:{
    //客服跳转
    onClickIcon() {
      this.$toast("客服还未上班哦~");
    },
    //店铺跳转
    onClickstore(){
       this.$router.push("home")
    },
    //倒计时
    showPopup() {
      this.show = true;
    },
    // 提交订单
    submitHandler(){
      let url = "/order/save";
      let data = {
        customerId:this.info.id,
        addressId: this.addressId,
        orderLines:this.orderLines
      }
      // console.log(data);
      post_obj_array(url,data).then(response =>{
        this.$toast("提交成功");
        this.$router.push("/manager/order")
      })
    },
    // 查询地址信息
    loadAddress(){
      let id = this.info.id;  
      let url = "/address/findByCustomerId?id="+id;
      get(url).then((response)=>{
        // 将查询到的地址信息绑定到address这个变量中
        this.addresses = response.data;
        // 将查询到的地址列表中第一个地址的id赋值给data中addressId,表示默认地址
        this.addressId = this.addresses[0].id;
      })
    }
  }
}
</script>
<style scoped>
.address{
  margin-left: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}

</style>