<template>
  <div class="alert">
    <h3>{{ x }} + {{ y }} = ?</h3>
    <hr>
    <div class="buttons">
      <button class="btn btn-success" v-for="number in answers">
        {{ number }}
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        x: mtRand(100, 200),
        y: mtRand(100, 200)
      }
    },
    computed: {
      answers() {
        var res = [this.x + this.y];

        return res;
      }
    }
  }

  function mtRand(min, max) {
    let diff = max - min;
    return Math.floor(Math.random() * (diff + 1)) + min;
  }

</script>

<style scoped>
  .alert {
    padding-top: 20px;
    background-color: #eee;
  }
  .buttons {
    display:  flex;
    justify-content: space-around;
  }
</style>
