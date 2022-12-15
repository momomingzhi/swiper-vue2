<template>
  <section class="menu">
    <swiper
      class="swiper"
      :options="swiperOption"
      @click-slide="clickSlide"
      :style="{ width: '100ps', border: '1px solid' }"
    >
      <swiper-slide
        v-for="(slideContent, index) in list"
        :key="index"
        :class="[isActive === index ? 'active' : '']"
      >
        <div>
          {{ slideContent.content }}
        </div>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div>
    </swiper>
  </section>
</template>

<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import "swiper/css/swiper.css";
export default {
  name: "swiper-example-loop",
  title: "Loop mode / Infinite loop",
  components: {
    Swiper,
    SwiperSlide,
  },
  created() {
    this.list = [
      {
        width: "6rem",
        content: "시세",
      },
      {
        width: "2rem",
        content: "재건축정보",
      },
      {
        width: "7rem",
        content: "요약",
      },
      {
        width: "2rem",
        content: "인테리어",
      },
      {
        width: "auto",
        content: "금액",
      },
      {
        width: "1rem",
        content: "입지",
      },
      {
        width: "3rem",
        content: "입지",
      },
      {
        width: "5rem",
        content: "입지",
      },
      {
        width: "1rem",
        content: "입지",
      },
      {
        width: "6rem",
        content: "입지333",
      },
    ];
  },
  mounted() {
    const $menu = document.querySelectorAll(".menu .swiper-slide >div");
    this.list.forEach((item, _idx) => {
      console.log({ item }, $menu);
      $menu[_idx].style.width = item.width;
      $menu[_idx].style.border = "1px solid";
    });
  },
  data() {
    return {
      list: [],
      isActive: 0,
      swiperOption: {
        slidesPerView: 5,
        spaceBetween: 10,
        loop: false,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
    };
  },
  methods: {
    clickSlide(index, reallyIndex) {
      this.isActive = index;
    },
  },
};
</script>

<style>
.menu .swiper-slide {
  cursor: pointer;
  width: auto !important;
}
.menu .swiper-wrapper {
  border: 1px solid red;
  width: 200px;
  transform: translate3d(0px, 0px, 0px);
}
.menu .active {
  background: #4373f4;
  /* width: auto !important; */
  /* padding: 0 1rem; */
  color: #fff;
  border-radius: 32px;
}
.menu .swiper-button-next {
  color: #ccc;
}
.menu .swiper-button-prev {
  color: #ccc;
}
</style>