<script>
import Input from './components/Input.vue'
import Listes from './components/Lists.vue'
import CryptoConvert from 'crypto-convert'
const convert = new CryptoConvert(/*options?*/);
export default{
  components:{Input,Listes},
  data(){
    return{
      error: "",
      amount: "",
      FirstCryptoValue: "",
      SecondCryptoValue: "",
      result : ""
    }
  },
  methods:{
    GetsValue(val){
      this.amount = val
    },
    GetFirstCryptoValue(val){
      this.FirstCryptoValue = val
    },
    GetSecondCryptoValue(val){
      this.SecondCryptoValue = val
    },
    async GetCourse(){
      if(this.amount == ""){
        this.error = "Ошибка! Введите значение"
        this.result = ""
        return false
      }
      else if(this.amount == 0){
        this.error = "Ошибка! Введите не нулевое значение"
        this.result = ""
        return false
      }
      else if(this.FirstCryptoValue == this.SecondCryptoValue || this.SecondCryptoValue == this.FirstCryptoValue){
        this.error = "Ошибка! Невозможно конвертировать в одинаковую валюту"
        this.result = ""
        return false
      }
      else if(this.FirstCryptoValue == "" || this.SecondCryptoValue == ""){
        this.error = "Ошибка! Вы не выбрали валюту"
        this.result = ""
      }
      else{
        this.error = ""
        await convert.ready(); //Wait for the initial cache to load
        if(this.FirstCryptoValue == "BTC" && this.SecondCryptoValue == "UsdT"){
          this.result = "Результат:" +  convert.BTC.USD(this.amount);
        }
        else if(this.FirstCryptoValue == "UsdT" && this.SecondCryptoValue == "BTC"){
          this.result = "Результат:" + convert.USD.BTC(this.amount);
        }
        else if(this.FirstCryptoValue == "ETH" && this.SecondCryptoValue == "UsdT"){
          this.result = "Результат:" + convert.ETH.USDT(this.amount);
        }
        else if(this.FirstCryptoValue == "ETH" && this.SecondCryptoValue == "BTC"){
          this.result = "Результат:" + convert.ETH.BTC(this.amount);
        }
        else if(this.FirstCryptoValue == "BTC" && this.SecondCryptoValue == "ETH"){
          this.result = "Результат:" + convert.BTC.ETH(this.amount);
        }
        else if(this.FirstCryptoValue == "UsdT" && this.SecondCryptoValue == "ETH"){
          this.result = "Результат:" + convert.USDT.ETH(this.amount);
        }
        else{
          return this.result = ""
        }
      }
    }
  }
}
</script>

<template>
  <h1 class="text-center mt-5 text-primary fw-bolder">Курс криптовалюты</h1>
  <Input :GetValue="GetsValue" :Course="GetCourse"/>
  <div class="d-flex justify-content-center mt-5">
    <Listes :GetCrypto="GetFirstCryptoValue" className="bg-dark"/>
    <Listes :GetCrypto="GetSecondCryptoValue" className="bg-dark"/>
  </div>
  <p class="error text-danger fs-2">{{ error }}</p>
    <p class="fs-2 text-info">{{ result }}</p>
</template>

<style scoped>
div{
  gap:50px;
  font-size: 30px;
  color: white;
}
ul{
  list-style: none;
  width:200px;
  height: max-content;
}
</style>