
/* eslint-disable */
<template>
<div id="main">
  <div class="container">
    <div class="left-pane" :class="{'open': open}"><div ref="left" class="title">TATA</div></div><!-- this comment removes the space
  --><div class="right-pane" :class="{'open': open}"><div ref="right" class="title">TOTO</div></div>
  </div>
  <div @click="toggle" ref="actionbtn" class="action-btn">
    <svg id="arrow" version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 129 129" xmlns:xlink="http://www.w3.org/1999/xlink" enable-background="new 0 0 129 129">
  <g>
    <path d="m40.4,121.3c-0.8,0.8-1.8,1.2-2.9,1.2s-2.1-0.4-2.9-1.2c-1.6-1.6-1.6-4.2 0-5.8l51-51-51-51c-1.6-1.6-1.6-4.2 0-5.8 1.6-1.6 4.2-1.6 5.8,0l53.9,53.9c1.6,1.6 1.6,4.2 0,5.8l-53.9,53.9z"/>
  </g>
</svg>
  </div>
</div>

</template>

<script>
/* eslint-disable */
import {TweenMax, Back} from 'gsap'
export default {
  name: 'hanna',
  data () {
    return {
      open: false,
      animating: false
    }
  },
  methods: {
    toggle () {
      console.log("hey")
      if (this.animating) {
        // avoid any action if button clicked when animated
        return
      }
      if (this.open){
        console.log("left");
                            TweenMax.to(this.$refs.left, 1, { fontSize: 30, ease: Sine.easeOut, autoRound: false, delay: 1})
                                                TweenMax.to(this.$refs.right, 1, { fontSize: 50, ease: Sine.easeOut, autoRound: false, delay: 1})



      } else {console.log("right")
                    TweenMax.to(this.$refs.left, 1, { fontSize: 50, ease: Sine.easeOut, autoRound: false, delay: 1})
                                                TweenMax.to(this.$refs.right, 1, { fontSize: 30, ease: Sine.easeOut, autoRound: false, delay: 1})


}
      this.open = !this.open
      this.animateButton()
    },
    animateButton () {
      this.animating = true

      // animate out
      const propsOut = {
        fontSize:20,
        scale: 0,
        ease: Back.easeIn,
        onComplete: this.animateIn
      }
      TweenMax.to(this.$refs.actionbtn, 0.2, propsOut)

    },
    animateIn () {
      // set new position
      TweenMax.set(this.$refs.actionbtn, this.actionBtnPosition)

      const propsIn = {
        delay: 0.4,
        scale: 1,
        ease: Back.easeOut
      }
      TweenMax.to(this.$refs.actionbtn, 0.2, propsIn)

      const propsRotation = {
        delay: 0.4,
        rotation: this.actionBtnRotation,
        onComplete: this.endedAnimating
      }
      
      TweenMax.to(this.$refs.actionbtn, 0.3, propsRotation)
    },
    endedAnimating () {
      this.animating = false
    }
  },
  computed: {
    actionBtnPosition () {
      const perc = this.open ? '70%' : '30%'
      const top = this.open ? '300px' : '500px'
      return {
        top: top,
        left: `calc(${perc} - 25px)`
      }
    },
    actionBtnRotation () {
      return this.open ? -180 : 0
    }
  }
}

</script>
<style scoped>

body {
  margin: 0px !important;
}
.main {
  display: flex;
  position: relative;
  ;
}
.container {
  height: 100vh;
  display: flex;
}
.left-pane {
  display: inline-block;
  background-color:#ffa299;
  width: 30%;
  height: 100%;
    position: relative;

}
.left-pane.open {
  width: 70%;
}
.right-pane {
  display: inline-block;
  width: 70%;
  height: 100%;
  background-color: 	#0e1111;
  position: relative;

  /* background-image: url("https://placeimg.com/1000/600/nature");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50% 50%; */
}
.right-pane.open {
  width: 30%;
}
.right-pane, .left-pane {
  transition: width 0.7s;
}
.action-btn {
  position: absolute;
  left: calc(30% - 25px);
  top: 450px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  color:white ;
  font-size: 40px;
  text-align: center;
  cursor: pointer;
}

#arrow {
fill: white;
}

.title {
    color: white;
    top: 80px;
    font-size: 30px;
    /* left: 0; */
    /* right: 0; */
    text-align: center;
    position: absolute;
    width: 100%;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

</style>
