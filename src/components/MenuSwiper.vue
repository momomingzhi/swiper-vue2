<template>
  <section>
    <swiper
      :modules="modules"
      :slides-per-view="3"
      :space-between="10"
      navigation
      @swiper="onSwiper"
      @slideChange="onSlideChange"
      @click="onClick"
    >
      <swiper-slide
        v-for="(slideContent, index) in slides"
        :key="index"
        :virtualIndex="index"
        >{{ slideContent }}</swiper-slide
      >
    </swiper>
  </section>
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
// import { Swiper, SwiperSlide, useSwiper } from "swiper/vue";

// Import Swiper styles
//import "swiper/css";

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      isClick: 0,
      swiperOptions: {
        //loop: true,
        // autoplay:{
        //   delay:1000
        // },
        // pagination: {
        //   el: ".swiper-pagination",
        // },
        // navigation: {
        //   nextEl: ".swiper-button-next",
        //   prevEl: ".swiper-button-prev",
        // },
      },
    };
  },
  setup() {
    const swiper = useSwiper();
    const slides = [
      "시세",
      "재건축정보",
      "예산",
      "인테리어",
      "요약정보",
      "단지글",
    ];
    const onSwiper = (swiper) => {
      //console.log(swiper);
    };
    const onSlideChange = () => {
      //console.log("slide change");
    };
    const onClick = (index) => {
      console.log("ㅎㅇㅎㅇ:", index.clickedIndex);
    };
    return {
      slides,
      onSwiper,
      onSlideChange,
      onClick,
      modules: [Navigation, Pagination, Scrollbar, A11y],
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
section {
  display: flex;
  margin: 2rem auto 0 auto;
  align-items: center;
  width: 80%;
  height: 10rem;
}
section .swiper {
  /* height: 100%; */
}
section .swiper-slide {
  text-align: center;
  padding: 2rem;
  display: flex; /* 내용을 중앙정렬 하기위해 flex 사용 */
  align-items: center; /* 위아래 기준 중앙정렬 */
  justify-content: center; /* 좌우 기준 중앙정렬 */
  background: #4373f4;
}
section .swiper-button-next {
  color: #ccc;
}

section .swiper-button-prev {
  color: #ccc;
}
</style>
