<template>
    <div class="painel">
      <h2 class="painel-titulo">{{ titulo }}</h2>
        <div class="painel-corpo">
            <slot>
            </slot>
            <!-- <img
                class="imagem-responsiva"
                :src="user.avatar"
                :alt="user.first_name + user.last_name"
                :title="user.first_name + user.last_name"
            /> -->
        </div>
    </div>
</template>

<script>
export default {
  props: ['titulo']
};
</script>

<style scoped>

.painel {
  padding: 0 auto;
  border: solid 1px grey;
  display: inline-block;
  margin: 0 10px;
  box-shadow: 2px 2px 10px grey;
  width: 150px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}

.painel .painel-titulo {
  font-size: 14px;
  text-align: center;
  border-bottom: solid 1px grey;
  background: mediumspringgreen;
  margin: 0;
  padding: 10px;
  text-transform: uppercase;
}
</style>