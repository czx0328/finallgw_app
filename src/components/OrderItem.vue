<template>
  <div class="order_item">
    <van-row class="header"> 
      <van-col span="12">订单编号: {{data.id}}</van-col>
      <van-col span="12" class="status">{{data.status}}</van-col>
    </van-row>
    <van-row>
      <van-col :span="24" :offset="1">
        <div v-if="data.waiter!=null">
          <van-icon name="friends-o" /><van-tag round type="primary">鉴别员姓名：</van-tag>
          {{data.waiter.realname}} 
        </div>
        <div v-if="data.waiter!=null">
          <van-icon name="phone-o" /><van-tag round type="primary">鉴别员联系方式：</van-tag>
          {{data.waiter.telephone}} 
        </div>
        <div v-if="data.orderLines != null"><van-icon name="bag-o" /><van-tag round type="primary">购买商品：</van-tag>
          <span 
            v-for="line in data.orderLines" 
            :key="line.id">
              {{line.product.name}}
          </span>
        </div>
        <div><van-icon name="balance-o" /><van-tag round type="primary">金额：</van-tag>{{data.total}}</div>
        <div><van-icon name="clock-o" /><van-tag round type="primary">购买时间：</van-tag>{{data.orderTime | datefmt}}</div>
        <div><van-icon name="wap-home-o" /><van-tag round type="primary">收货地址:</van-tag>
          {{data.address.province}} 
          {{data.address.city}}
          {{data.address.area}}
          {{data.address.address}}
        </div>
      </van-col>
    </van-row>
    <div class="text-right">
      共计 {{data.orderLines.length}} 个商品，合计￥ {{data.total}}
    </div>
  </div>
</template>
<script>
export default {
  props:{
    data:{type:Object}
  }
}
</script>
<style scoped>
.order_item {
  margin: .5em 1em;
  padding: .5em;
  border-radius: 5px;
  background: #ffffff;
}
.order_item .header {
  line-height: 2.5em;
  font-size: 14px;
}
.order_item .header .status {
  text-align: right;
  font-size: 12px;
  color: #fd621f;
}
.order_item img {
  width: 100%;
  border-radius: 3px;
}


</style>