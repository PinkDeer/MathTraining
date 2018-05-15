<template>
  <div class="training">
    <h1>Math training</h1>
    <hr>
    <div calss="box">
      <transition name="flip" mode="out-in">
        <app-start-screen
          v-if="state == 'start'"
          @onStart="onStart">
        </app-start-screen>
        <app-question v-else-if="state == 'question'"
          @success="onQuestSuccess"
          @error="onQuestError"
        ></app-question>
        <app-message v-else-if="state == 'message'"
          :type="message.type"
          :text="message.text"
          @onNext="onNext">
        </app-message>
        <app-resault-screen v-else-if="state == 'resaults'"></app-resault-screen>
        <div v-else>Unknown state</div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      state: 'start',
      stats: {
        succeses: 0,
        error: 0
      },
      message: {
        type: '',
        text: ''
      }
    }
  },
  computed: {
    questDone(){
      return this.stats.success + this.stats.error;
    }
  },
  methods: {
    onStart(){
      this.state = 'question';
    },
    onQuestSuccess(){
      this.state = 'message';
      this.message.text = 'Good Job!'
      this.message.type = 'success'
    },
    onQuestError(msg){
      this.state = 'message';
      this.message.text = msg;
      this.message.type = 'warning'
    },
    onNext(){
      this.state = 'question';
    }
  }
}
</script>

<style scoped>
  .training {
    max-width: 700px;
    margin: 20px auto;
  }

  .flip-enter {

  }
  .flip-enter-active {
    animation: flipInX 0.3s linear;
  }
  .flip-leave {

  }
  .flip-leave-active {
    animation: flipOutX 0.3s linear;
  }

  @keyframes flipInX {
    from{transform: rotateX(90deg);}
    to{transform: rotateX(0deg);}
  }
  @keyframes flipOutX {
    from{transform: rotateX(0deg);}
    to{transform: rotateX(90deg);}
  }

</style>
