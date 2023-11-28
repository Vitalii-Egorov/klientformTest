<template>
  <div class="container">
      <div class="container__title">Форма создания Клиента</div>
      <sign-up />
  </div>
</template>

<script>
import SignUp from './components/SingUp.vue'

export default {
  name: 'App',
  components: {
    SignUp,
  }
}
</script>

<style lang="scss">
.container {
width: 500px;
border: 1px solid #000;
margin: 0 auto;
padding-bottom: 20px;


&__title {
background: #bdde1570;
text-align: center;
border-bottom:1px solid #000 ;
padding: 10px 0px;
margin-bottom: 30px;
}
}

</style>
