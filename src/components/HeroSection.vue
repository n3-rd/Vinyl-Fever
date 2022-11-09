<template>
  <div class="main-screen background">
    <div class="hero-text main-screen-title font-display">VINYL FEVER</div>
    <div class="vinyl-container">
      <div class="vinyl">
        <div class="vinyl-line">
          <div
            class="vinyl-inner"
            data-lg-scroll
            data-lg-scroll-animate="{'rotateZ': ['0deg', '360deg']}"
          >
            <div class="vinyl-hole"></div>
            <img
              src="https://loremflickr.com/420/340/album,art,cover/all"
              class="vinyl-image"
              crossorigin="anonymous"
            />
          </div>
        </div>
      </div>
    </div>
    <HeroAbout class="hero-text" />
    <VinylSale />
    <FooterSection />
  </div>
</template>

<style lang="scss">
@use "../assets/media-queries" as *;
.background {
  min-height: 100vh;
  background-color: #f5f5f5;
  .main-screen-title {
    font-size: 4vw;
    text-align: center;
    padding-top: 2rem;
    font-weight: 800;
  }
}
.vinyl-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .vinyl {
    height: 35rem;
    width: 35rem;
    background-color: #000;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    .vinyl-line {
      height: 26rem;
      width: 26rem;
      border-radius: 50%;
      border: 1px #fff solid;
      display: flex;
      justify-content: center;
      align-items: center;
      .vinyl-inner {
        height: 22rem;
        width: 22rem;
        background-color: #fff;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        .vinyl-hole {
          height: 3rem;
          width: 3rem;
          background-color: #000;
          border-radius: 50%;
          position: absolute;
          border: 1px #fff solid;
        }
        .vinyl-image {
          height: 100%;
          width: 100%;
          border-radius: 50%;
          object-fit: cover;
        }
      }
    }
  }
}
@include media-query(mobile) {
  .hero-text {
    font-size: 7vw !important;
    line-height: 1.8rem;
    padding-top: 0.4rem;
    padding-bottom: 0.4rem;
  }
  .vinyl {
    height: 17rem !important;
    width: 17rem !important;
  }
  .vinyl-line {
    height: 12rem !important;
    width: 12rem !important;
  }
  .vinyl-inner {
    height: 9rem !important;
    width: 9rem !important;
  }
  .vinyl-hole {
    height: 1.5rem !important;
    width: 1.5rem !important;
  }
}
</style>

<script lang="js">
import luge from "@waaark/luge";
import ColorThief from 'colorthief'
import Lenis from '@studio-freight/lenis'
import HeroAbout from './HeroAbout.vue'
import VinylSale from "./VinylSale.vue";
import FooterSection from "./FooterSection.vue";
const smoothScroll = ()=>{
    const lenis = new Lenis({
  duration: 1.2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)), // https://www.desmos.com/calculator/brs54l4xou
  direction: 'vertical', // vertical, horizontal
  gestureDirection: 'vertical', // vertical, horizontal, both
  smooth: true,
  mouseMultiplier: 1,
  smoothTouch: true,
  touchMultiplier: 2,
  infinite: false,
})


function raf(time) {
  lenis.raf(time)
  requestAnimationFrame(raf)
}

requestAnimationFrame(raf)
}


export default {
    data(){
        return {
            randomSeed: Math.floor(Math.random() * 100000)
        }
    },
    components: {
    HeroAbout,
    VinylSale,
    FooterSection,
},
    methods: {
        getDominantColor() {
            const colorThief = new ColorThief()
            const image = document.querySelector('.vinyl-image')
            const color = colorThief.getColor(image)
            const rgb = `rgb(${color[0]}, ${color[1]}, ${color[2]})`;
            document.querySelector('.main-screen').style.backgroundColor = rgb
            document.querySelector('.vinyl-hole').style.backgroundColor = rgb

            const heroText = document.querySelector('#app');
            console.log(heroText)

            // adjust text color based on background color
            const brightness = Math.round(((parseInt(color[0]) * 299) +
                (parseInt(color[1]) * 587) +
                (parseInt(color[2]) * 114)) / 1000);
            if (brightness > 125) {
              heroText.style.color = 'black';
            } else {
              heroText.style.color = 'white';
            }

            // adjust vinyl line color based on background color
            const vinylLine = document.querySelector('.vinyl-line')
            vinylLine.style.borderColor = rgb
        },
    },
  mounted() {
    luge.lifecycle.refresh();
    window.onload = () => {
        this.getDominantColor();
        smoothScroll();
    }
  },
};
</script>
