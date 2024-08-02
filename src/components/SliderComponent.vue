<template>
  <div class="slider">
    <div
      class="slide"
      v-for="(slide, index) in slides"
      :key="index"
      :style="{ backgroundColor: slide.backgroundColor }"
      :class="{ active: index === currentIndex }"
    >
      <div v-if="slide.topImage" class="top-image-container">
        <img :src="slide.topImage" class="top-image" alt="Top Image" />
        <div class="drop-container">
          <div class="drop">
            Lorem ipsum dolor sit amet
          </div>
        </div>
      </div>
      <div class="text-and-side-image">
        <div class="text-container">
          <div class="title">
            <div class="line1">LOREM IPSUM</div>
            <div class="line2">LOREM IPSUM DOLOR —</div>
            <div class="line3">LOREM</div>
            <div class="line4">IPSUM !</div>
          </div>
          <p class="subtitle">{{ slide.subtitle }}</p>
        </div>
        <img v-if="slide.sideImage" :src="slide.sideImage" class="side-image" alt="Side Image" />
      </div>
      <img v-if="slide.starImage" :src="slide.starImage" class="star-image" alt="Star Image" />
    </div>
    <button class="nav-button" @click="nextSlide">
      <div class="circle-container">
  <svg viewBox="0 0 200 200" class="circle-svg">
    <circle cx="100" cy="100" r="95" fill="none" stroke="white" stroke-width="0" />
    <path id="textPath" d="M 100,100 m -95,0 a 95,95 0 1,1 190,0 a 95,95 0 1,1 -190,0" fill="none" />
    <text font-family="Arial" font-size="14" fill="white">
      <textPath xlink:href="#textPath" startOffset="0%">
        ДИВИТИСЯ ДАЛІ ДИВИТИСЯ ДАЛІ ДИВИТИСЯ ДАЛІ ДИВИТИСЯ ДАЛІ ДИВИТИСЯ ДАЛІ ДИВИТИСЯ ДАЛІ
      </textPath>
    </text>
  </svg>
  <span class="arrow">→</span>
</div>



    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentIndex: 0,
      slides: [
        {
          title: "lorem ipsum\nLorem ipsum dolor — \nLorem ipsum",
          subtitle: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
          backgroundColor: "#027D84",
          topImage: require('@/assets/origin.jpg'),
          starImage: require('@/assets/Dawn1.png'),
          sideImage: require('@/assets/Dog.png'),
        },
        {
          title: "lorem ipsum\nLorem ipsum dolor — \nLorem ipsum",
          subtitle: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
          backgroundColor: "#4A989A",
          topImage: require('@/assets/origin.jpg'),
          starImage: require('@/assets/Dawn.png'),
          sideImage: require('@/assets/Dog.png'),
        },
        {
          title: "lorem ipsum\nLorem ipsum dolor — \nLorem ipsum",
          subtitle: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
          backgroundColor: "#AFB3B4",
          topImage: require('@/assets/origin.jpg'),
          starImage: require('@/assets/Dawn2.png'),
          sideImage: require('@/assets/Dog.png'),
        },
      ],
    };
  },
  methods: {
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
    },
  },
  mounted() {
    setInterval(this.nextSlide, 3000); // Менять слайд каждые 3 секунды
  },
};
</script>

<style scoped>
.slider {
  position: relative;
  display: flex;
  justify-content: center;
  overflow: hidden;
  width: 1440px; /* Ширина слайдера */
  height: 708px; /* Высота слайдера */
}

.slide {
  position: absolute;
  top: 0;
  width: 100%;
  height: 100%;
  transition: transform 0.5s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  overflow: hidden;
}

.slide:not(.active) {
  transform: translateX(100%);
}

.top-image-container {
  position: relative;
  left: 88px;
  width: 1134px; /* Ширина контента */
  height: 100%;
}

.top-image {
  position: absolute;
  top: 0;
  width: 506px;
  z-index: 1;
}

.drop-container {
  position: relative;
  left: 20px;
  top: -83px;
  font-size: 18px;
  width: 463.85px;
  height: 240.79px;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
}

.drop {
  color: #fff;
  width: 265px; 
  height: 21px; 
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 18px; 
  padding: 0; 
  box-sizing: border-box;
}

.text-and-side-image {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 1134px; /* Ширина контента */
  height: 100%;
  position: relative;
  z-index: 3;
}

.text-container {
  width: 920px;
  bottom: 70px;
  position: relative;
  right: 340px;
  text-align: center;
  margin: 0 20px; /* Отступы вокруг текста */
}

.title {
  margin-bottom: 20px; /* Отступ между заголовком и подзаголовком */
  display: flex;
  flex-direction: column;
}

.line1 {
  display: flex;
  font-family: 'Roboto', sans-serif;
  font-weight: bold;
  font-size: 60px;
  color: #FFFFFF;
  margin: 0;
}

.line2 {
  position: relative;
  right: 42px;
  font-family: 'Roboto', sans-serif;
  font-weight: regular;
  font-size: 60px;
  color: #FFFFFF;
  -webkit-text-stroke: 2px #000000;
  margin: 0;
}

.line3 {
  position: relative;
  right: 40px;
  font-family: 'Roboto', sans-serif;
  font-weight: regular;
  font-size: 60px;
  color: #FFFFFF;
  margin: 0;
}

.line4 {
  position: relative;
  right: 190px;
  font-family: 'Roboto', sans-serif;
  font-weight: regular;
  font-size: 60px;
  color: #FFFFFF;
  margin: 0;
}

.subtitle {
  position: relative;
  left: 300px;
  text-transform: uppercase;
  font-family: 'Roboto', sans-serif;
  font-weight: medium;
  font-size: 15px;
  color: #FFFFFF;
  width: 278px;
  height: 66px;
  margin: 0;
}

.side-image {
  width: 642px; /* Настройте по необходимости */
  height: 646px;
  position: absolute;
  z-index: -1;
}

.star-image {
  position: absolute;
  left: 0;
  width: 160px;
  height: 160px;
  z-index: 2;
}

.nav-button {
  position: absolute;
  bottom: 300px;
  right: 100px;
  display: flex;
  align-items: center;
  background: transparent;
  border: none;
  color: #fff;
  cursor: pointer;
  z-index: 4;
}

.circle-container {
  position: relative;
  width: 200px;
  height: 100px;
}

.circle-svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  animation: spin 10s linear infinite;
}

.arrow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 24px;
  color: #fff;
  z-index: 1;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@media (max-width: 768px) {
  .slider {
    width: 100%;
    height: auto; /* Адаптивная высота */
  }

  .top-image {
    width: 100%;
    height: auto;
  }

  .star-image {
    width: 100px;
    height: 100px;
  }

  .side-image {
    width: 150px; /* Настройте по необходимости */
  }
}
</style>
