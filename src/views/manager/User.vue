<template>
  <div class="user">
    <div class="header">
      <div class="photo">
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1603969691628&di=0ec53b8fd5b21592ab5dba1d31710d7f&imgtype=0&src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_bt%2F0%2F11242855741%2F1000.jpg" alt=""/>
      </div>
      <div class="name">{{info.name}}</div>
    </div>
    
    <van-cell title="🏠常用地址" is-link to="/manager/address" />
    <van-cell title="📋所有订单" is-link to="/manager/order" />
    <van-cell title="📋物流信息" is-link to="/deliverd" />

    <div class="btn" @click="logoutHandler">
      退出
    </div>
  </div>
</template>
<script>
import {mapState, mapActions} from 'vuex'
export default {
  methods:{
    ...mapActions('user',['logout']),
    toAddressHandler(){
      // this.$router.push({path:'/manager/address'})
    },
    logoutHandler(){
      this.logout()
      .then(()=>{
        this.$router.push({path:'/login'})
      })
    }
  },
  computed:{
    ...mapState("user",["info"])
  }
}
</script>

<style scoped>
.header {
  
  /* padding-top: 46px; */
  text-align: center;
  background: #ffadfb;
  margin-bottom: 2em;
}

.header .photo {
  margin: 0 auto;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  box-sizing: border-box;
  /* border:1px solid #1659a0; */
  overflow:hidden;
  padding: 1em;
}
.header .name {
  line-height: 3em;
  font-size: 16px;
  color: #020202;

}
.header .photo img {
 width: 100%;
 border-radius: 50%;
}

.btn {
  width: 90%;
  margin: 1em auto;
  line-height: 3em;
  text-align: center;
  border: 1px solid #ededed;
  border-radius: 1.5em;
}

</style>