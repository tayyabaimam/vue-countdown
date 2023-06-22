<template>
  <div>
    <Counter
      :year="2023"
      :month="6"
      :date="22"
      :hour="6"
      :minute="53"
      :second="0"
      :millisecond="0"
    />
  </div>
</template>

<script>
import Counter from "../Counter.vue";
export default {
  components: { Counter },
};
</script>

<style lang="scss" scoped></style>
