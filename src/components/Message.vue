<template>
  <div class="mess-age">
    <p>Message from component - {{ message }}</p>
  </div>
</template>

 <script>
export default {
  props: {
    //здесь в пропсах пишем что мы принимаем из др.компонентов, в данном случае это message
    message: {
      type: String,
      require: true,
      // default: 'любое сообщение по умолчанию, не обязательный параметр пропсов'
    },
  },
};
</script>

<style lang="scss" scoped>
/*scoped ограничивает область видимости стилей относительно одного компонента */
.mess-age {
  text-align: center;
  padding: 20px;
}

p {
  color: rgb(86, 34, 231);
  font-weight: 800;
}
</style>

