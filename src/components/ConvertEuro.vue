<template>
  <div class="converter">
    <label>em R$:</label>
    <span>
      {{
        value.toLocaleString("pt-br", {
          style: "currency",
          currency: "BRL",
        })
      }}</span
    >
  </div>
</template>

<script>
export default {
  props: {
    value: Number,
  },
};
</script>

<style lang="scss" scoped>
.converter {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 20px 0;
  label {
    font-size: 14px;
    font-weight: 600;
  }
  span {
    margin: 0 7px;
    font-size: 22px;
    font-weight: 600;
  }
}
</style>
