<script>
export default{
  props:{
    GetCrypto:{
      type:Function,
      required:true
    }
  },
  data(){
    return{
      current: ""
    }
  },
  methods:{
    GetFullCrypto(val){
      this.GetCrypto(val)
      this.current = val
    }
  }
}
</script>

<template>
  <ul>
    <li v-on:click="GetFullCrypto('BTC')" :className="current == 'BTC' ? 'text-danger' : ''">BTC</li>
    <li v-on:click="GetFullCrypto('UsdT')" :className="current == 'UsdT' ? 'text-danger' : ''">UsdT</li>
    <li v-on:click="GetFullCrypto('ETH')" :className="current == 'ETH' ? 'text-danger' : ''">ETH</li>
  </ul>
</template>

<style scoped>

</style>