<template>
  <div class="container">
    <users-list></users-list>
  </div>

  <div class="container">
    <div class="block" :class="{ animate: animatedBlock }"></div>
    <button @click="animateBlock()">Animate</button>
  </div>

  <div class="container">
    <transition 
    :css="false" 
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter" 
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    @enter-cancelled="enterCancelled"
    @leave-cancelled="leaveCancelled"
    >
      <p v-if="paraIsVisible">This is only sometimes visible...</p>
    </transition>
    <button @click="toggleParagraph()">Toggle Paragraph</button>
  </div>
  
  <div class="container">
    <transition name="fade-button" mode="out-in">
      <button @click="showUsers()" v-if="!usersAreVisible">Show Users</button>
      <button @click="hideUsers()" v-else>Hide Users</button>
    </transition>
  </div>
  
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  

  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>  
</template>



<script>
import UsersList from './components/UsersList.vue';
export default {
  components: {UsersList},
  data() {
    return { 
      animatedBlock: false,
      dialogIsVisible: false,
      paraIsVisible: false,
      usersAreVisible: false,
      enterInterval: null,
      leaveInterval: null
    };
  },
  methods: {
    enterCancelled(el) {
      console.log(el);
      clearInterval(this.enterInterval);
    },
    leaveCamcelled(el) {
      console.log(el);
      clearInterval(this.leaveInterval);
    },
    beforeEnter(el) {
      console.log('before enter');
      console.log(el);
      el.style.opacity = 0;
    },
    enter(el, done) {
      console.log('enter');
      console.log(el);
      let round = 1
      this.enterInterval = setInterval(() => {
        el.style.opacity = round * .01;
        round++
        if (round > 100) {
          clearInterval(this.enterInterval);
          done();
        }
      }, 20);
    },
    afterEnter(el) {
      console.log('after enter');
      console.log(el);
    },
    beforeLeave(el) {
      console.log('before leave');
      console.log(el);
      el.style.opacity = 1;
    },
    leave(el, done) {
      console.log('leave');
      console.log(el);
      let round = 1;
      this.leaveInterval = setInterval(() => {
        el.style.opacity = 1 - round * 0.01;
        round++
        if (round > 100) {
          clearInterval(this.leaveInterval);
          done();
        }        
      }, 20);
    },
    afterLeave(el) {
      console.log('after leave');
      console.log(el);
    },






    showUsers() {
      this.usersAreVisible = true;
    },

    hideUsers() {
      this.usersAreVisible = false;
    },

    animateBlock() {
      this.animatedBlock = true;
    },

    toggleParagraph(){
      this.paraIsVisible = !this.paraIsVisible;
    },

    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  list-style: none;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}

.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition: transform .5s ease-in-out; */
}

.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}

.animate{
  /* transform: translateX(-50px); */
  animation: slide-fade .7s ease-out forwards;
}

/* .para-enter-from {
  opacity: 0;
  transform: translateY(-30px);
}

.para-enter-active {
  transition: all 3s ease-out;
}

.para-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.para-leave-from{
  opacity: 1;
  transform: translateY(0);
}

.para-leave-active{
  transition: all .3s ease-in;
}

.para-leave-to{
  opacity: 0;
  transform: translateY(30px);
} */


.fade-button-enter-from,
.fade-button-leave-to{
  opacity: 0;
}

.fade-button-enter-active{
  transition: opacity .3s ease-out;
}

.fade-button-leave-active{
  transition: opacity .3s ease-in;
}

.fade-button-enter-to,
.fade-button-leave-from{
  opacity: 1;
}



@keyframes slide-scale {
  0% {
    transform: translateX(0) scale(1);
  }
  70% {
    transform: translateX(-120px) scale(1.1);
  }
  100% {
    transform: translateX(-150px) scale(1);
  }
}
</style>