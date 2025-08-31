<script>
export default{
  props:{
    GetValue:{
      type:Function,
      required:true
    },
    Course:{
      type:Function,
      required:true
    }
  }
}
</script>

<template>
  <form method="post" class="d-flex flex-column align-items-center mt-5 bg-dark">
    <label class="fs-1 text-primary">Введите значение:</label>
    <input v-on:input="GetValue($event.target.value)" min="0" type="number" class="form-control w-50 mt-5">
    <button type="button" v-on:click="Course()" class="btn btn-primary btn-lg mt-5">Конвертировать</button>
  </form>
</template>

<style scoped>
form{
    border-radius: 50px;
}
</style>