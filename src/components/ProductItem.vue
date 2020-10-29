<template>
  <!-- emit 发射，将组件上接受到的click事件发射给发组件中的click事件 -->
  <div class="product_item" @click="$emit('click')">
    <van-row>
      <van-col :span="4">
        <img v-if="data.photo" :src="data.photo" alt="">
        <img v-else src="../assets/service.png" alt="">
      </van-col>

      <van-col :offset="1" :span="19">
        <div><van-icon name="new-arrival-o" color=" 	#FF0000" size="2rem" /> <strong> {{data.name}}</strong><van-tag class="tag" color=" 	#000000"><van-icon name="label-o" />{{data.status}}</van-tag></div>
        <div> {{data.description}}</div>
         <div style="color:red;float:right"> 💰{{data.price}}</div>
      </van-col>
    </van-row>
  </div>
</template>
<script>
export default {
  props:['data'],
  data(){
    return {
      value:0
    }
  },
  methods:{
   
  }
}
</script>
<style scoped>
.product_item {
  margin:.5em 1em;
  padding: .5em;
  border-radius: 5px;
  height: 80px;
  border: 1px dotted #ccc;
}

.product_item img {
  width: 100%;
  border-radius: 3px;
}
.tag{
 float: right;
 margin-top: 10px;
}

</style>