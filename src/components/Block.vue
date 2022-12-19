<template>
  <div v-if="showBlock" class="block" @click="stopTimer">click me</div>
</template>

<script>
export default {
  name: "Block",
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  props: ["delay"],
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10; //Makes the timer count in 10
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer); // This stops the timer
      this.$emit("end", this.reactionTime); // $emit is how we send data from a child component up ('name it anything', whatever you are sending)
    },
  },
};
</script>

<style scoped>
.block {
  width: 400px;
  border-radius: 20px;
  background: black;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
