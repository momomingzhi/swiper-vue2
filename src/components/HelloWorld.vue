<template>
  <main>
    <swiper
      :slides-per-view="1"
      :space-between="50"
      navigation
      :pagination="{ clickable: true }"
      @swiper="onSwiper"
      @slideChange="onSlideChange"
    >
      <swiper-slide>Slide 1</swiper-slide>
      <swiper-slide>Slide 2</swiper-slide>
      <swiper-slide>Slide 3</swiper-slide>
      <swiper-slide>Slide 4</swiper-slide>
      <div class="swiper-button-prev swiper-btn-prev" slot="button-prev"></div>
      <div class="swiper-button-next swiper-btn-next" slot="button-next"></div>
    </swiper>
  </main>
</template>
<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import "swiper/css/swiper.css";
// import { Navigation, Pagination, Scrollbar, A11y } from "swiper";

// import "swiper/css";
// import "swiper/css/navigation";
// import "swiper/css/pagination";
// import "swiper/css/scrollbar";
// import "swiper/css/effect-fade";
// // Import Swiper Vue.js components
// import { Swiper, SwiperSlide } from "swiper/vue";

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      swiperOptions: {
        loop: true,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
    };
  },
  setup() {
    const onSwiper = (swiper) => {
      console.log(swiper);
    };
    const onSlideChange = () => {
      console.log("slide change");
    };
    return {
      onSwiper,
      onSlideChange,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
main {
  display: flex;
  margin: 0 auto;
  align-items: center;
  width: 80%;
  height: 20rem;
}
main .swiper {
  height: 100%;
  box-shadow: 0 0 20px #ccc inset;
}
main .swiper-slide {
  text-align: center;
  display: flex; /* 내용을 중앙정렬 하기위해 flex 사용 */
  align-items: center; /* 위아래 기준 중앙정렬 */
  justify-content: center; /* 좌우 기준 중앙정렬 */
}
</style>
