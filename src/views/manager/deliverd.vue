<template>

    <van-steps direction="vertical" :active="0">
        <div><p>订单编号: 1017
运输中
鉴别员姓名： 王子久
鉴别员联系方式： 16672389721
购买商品： 男式西服
金额：33
购买时间：2020-02-24 08:24:54
收货地址: 河南 商丘 永城 邮局 </p></div>
  <van-step class="step">
    <h4>【杭州】杭州中转站已揽收</h4>
    <p>2020-10-30 12:40</p>
  </van-step>
  <van-step>
    <h4>【浙江】浙江运输中心已发出</h4>
    <p>2020-10-28 10:00</p>
  </van-step>
  <van-step>
    <h4>快件已发货</h4>
    <p>2020-10-28 09:30</p>
  </van-step>
</van-steps>
</template>
<style scoped>

</style>