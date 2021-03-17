<template>
  <q-page class="mysites-page">
    <div v-if="mySitesStatus === 'confirm'">
      <div class="title">Для работы с сайтами и блоками Вам необходимо подтвердить свой электронный адрес, указанный при регистрации.</div>
      <p class="about">
        Пожалуйста, перейдите по ссылке из письма;<br> 
        Если письма со ссылкой нет в папке “Входящие”, то проверьте папку “Спам”. Если письмо Вам не пришло, то напишите нам в чат и мы Вам   поможем.
      </p>
    </div>

    <div v-if="mySitesStatus === 'block'">
      <div class="title block">Аккаунт заблокирован</div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      mySitesStatus: 'block', // 'confirm', 'block'
    }
  }
}
</script>


<style lang="scss">
  .q-page {
    padding: 40px 40px 0;
  }

  .mysites-page {
    .title {
      font-weight: 500;
      font-size: 18px;
      line-height: 22px;
      margin: 0px 0px 24px 0px;
      color: #12284C;

      &.block {
        color: #A64541;
      }
    }

    .about {
      font-size: 18px;
      line-height: 32px;
      color: #12284C;
      margin: 0;      
    }
  }
</style>
