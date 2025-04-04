<template>
    <div class="slider-container">
      <div class="slideshow-wrapper">
        <div 
          v-for="(slide, index) in slides"
          :key="index"
          class="slide-item"
          :style="{ display: index === slideIndex ? 'block' : 'none' }"
        >
          <img :src="slide" class="mySlides" />
          <div class="slide-caption">
            {{ captions[index] }}
          </div>
        </div>
      </div>  
      <br />

      <div class="controls" style="text-align: center">
        <div class="nav-buttons">
          <button class="nav-button" @click="plusDivs(-1)">❮ Prev</button>
          <button class="nav-button" @click="plusDivs(1)">Next ❯</button>
        </div>
  
        <div class="indicators">
          <button
            v-for="(slide, index) in slides"
            :key="'btn-' + index"
            class="indicator"
            :class="{ active: index === slideIndex }"
            @click="currentDiv(index)"
          >
            {{ index + 1 }}
          </button>
        </div>
      </div>
    </div>
  </template>
  
<script>

  export default {
    name: "Skill",
    data() {
      return {
        slideIndex: 0,
        slides: ["/public/python_logo.webp",
                 "/public/arduino_logo.svg",
                 "/public/html_logo.png",
                 "/public/CSS_logo.png",
                 "/public/javascript-logo.webp",
                 "/public/CPP_logo.png",
                 "/public/Java_logo.png",
                 "/public/microsoft_logo.png"
                ],
        captions: [
          "Python Programming",
          "Arduino Skill",
          "HTML Programming",
          "CSS Programming",
          "JavaScrip Programming",
          "CPP Programming",
          "Java Programming",
          "Office Program of Microsoft"

        ]
      };
    },
    methods: {
      plusDivs(n) {
        this.slideIndex =
          (this.slideIndex + n + this.slides.length) % this.slides.length;
      },
      currentDiv(n) {
        this.slideIndex = n;
      },
    },
  };
  </script>
  
  <style>
  .title {
    background-color: rgb(172, 172, 172);
  }
  
  .slider-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 70vh;
    padding: 20px;
  }
  
  .slideshow-wrapper {
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
    position: relative;
  }
  
  .slide-item {
    position: relative;
    width: 100%;
  }
  
  .mySlides {
    max-width: 100%;
    max-height: 400px;
    object-fit: contain;
    display: block;
    width: 100%;
    margin-bottom: 100px;
    margin-top: 110px;
  }
  
  .slide-caption {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    text-align: center;
    color: white;
    background-color: rgba(0, 0, 0, 0.5);
    padding: 10px;
    font-size: 1.5em;
    bottom: -80px;
  }
  
  .controls {
    margin-top: 20px;
    width: 100%;
    max-width: 800px;
  }
  
  .nav-buttons {
    margin-bottom: 15px;
  }
  
  .nav-button {
    padding: 8px 16px;
    margin: 0 10px;
    background-color: #f1f1f1;
    border: none;
    cursor: pointer;
    border-radius: 4px;
  }
  
  .nav-button:hover {
    background-color: #ddd;
  }
  
  .indicators {
    display: flex;
    justify-content: center;
    gap: 10px;
  }
  
  .indicator {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    border: none;
    background-color: #f1f1f1;
    cursor: pointer;
  }

  .indicator.active {
    background-color: red;
  }
  </style>