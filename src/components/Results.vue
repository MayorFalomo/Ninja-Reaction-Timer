<template>
  <p>
    Reaction Time: <span>{{ score }}ms</span>
  </p>
  <!-- <p>{{ rank }}</p> -->
  <slot></slot>
</template>

<script>
export default {
  name: "Results",
  data() {
    return {
      rank: null,
    };
  },
  props: ["score"],
  mounted() {
    if (this.score < 250) {
      this.rank = "Ninja Fingers";
    } else if (this.score <= 400) {
      this.rank = "Rapid Reflexes ";
    } else {
      this.rank = "Butter Fingers";
    }
  },
};
</script>

<style></style>
