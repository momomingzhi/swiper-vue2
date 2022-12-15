
<template>
  <section class="two">
    <swiper
      class="swiper2"
      :options="swiperOption2"
      @click-slide="clickSlide"
      @slideChange="slideChange"
      ref="menuSwiper"
    >
      <swiper-slide
        v-for="(slideContent, index) in list"
        :key="index"
        :class="[isActive === index ? 'active' : '']"
      >
        {{ slideContent }}
      </swiper-slide>
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div>
    </swiper>
    <swiper
      class="swiper content"
      :options="swiperOption"
      ref="mySwiper"
      @slideChange="changeCardSlide"
    >
      <swiper-slide v-for="(slideContent, index) in list" :key="index">
        <component :is="dynamicComponent" v-bind:index="index"></component>
      </swiper-slide>
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div>
    </swiper>
  </section>
</template>

<script>
import TwoSwiperCard from "./TwoSwiperCard.vue";
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import "swiper/css/swiper.css";

export default {
  name: "swiper-example-loop",
  title: "Loop mode / Infinite loop",
  components: {
    Swiper,
    SwiperSlide,
    TwoSwiperCard,
  },
  created() {
    this.list = ["98m", "108m", "123m", "152m", "176m", "200m", "230m"];
    // const emptyArr = Array.from(
    //   { length: this.previewCount - (this.list.length % this.previewCount) },
    //   () => ""
    // );
    // this.list.push(...emptyArr);
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.$swiper;
    },
    menuSwiper() {
      return this.$refs.menuSwiper.$swiper;
    },
  },
  props: {
    previewCount: {
      type: Number,
    },
  },
  data() {
    return {
      list: [],
      isActive: 0,
      dynamicComponent: TwoSwiperCard,
      swiperOption: {
        slidesPerView: 1,
        spaceBetween: 10,
        slidesPerGroup: 1,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
      swiperOption2: {
        slidesPerView: this.previewCount,
        spaceBetween: 10,
        slidesPerGroup: 1,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
    };
  },

  methods: {
    clickSlide(index, reallyIndex) {
      this.swiper.slideTo(index, 1000, false);
      //this.menuSwiper.slideNext(1000, true);
      this.isActive = index;
      console.log("나옴", index, this.menuSwiper.activeIndex);
    },
    changeCardSlide() {
      const menuSwiper = this.menuSwiper;
      const cardSwiper = this.swiper;
      menuSwiper.slideTo(cardSwiper.activeIndex, 1000, false);
      this.isActive = cardSwiper.activeIndex;
      console.log(cardSwiper, menuSwiper);
      // this.isActive > 0
      //   ? menuSwiper.slideNext(1000, true)
      //   : menuSwiper.slidePrev(1000, true);
    },
    repeatFunc(count, callback) {
      for (let i = 0; i < Math.abs(count); i++) {
        callback();
      }
    },
    slideChange(data) {
      const menuSwiper = this.menuSwiper;
      const diff = menuSwiper.clickedIndex - menuSwiper.activeIndex;
      console.log("ddd:", menuSwiper.clickedIndex, menuSwiper.activeIndex);
      // if (diff <= 0) {
      //   this.repeatFunc(diff, () => menuSwiper.slidePrev(1000, true));
      // }
      // diff < 0
      //   ? this.repeatFunc(diff, () => menuSwiper.slidePrev(1000, true))
      //   : this.repeatFunc(diff, () => menuSwiper.slideNext(1000, true));
    },
  },
};
</script>

<style>
.two {
  margin: 3rem 0 0;
}
.two .swiper2 .swiper-slide {
  cursor: pointer;
}
.two .swiper2 .active {
  text-align: center;
  display: flex; /* 내용을 중앙정렬 하기위해 flex 사용 */
  align-items: center; /* 위아래 기준 중앙정렬 */
  justify-content: center; /* 좌우 기준 중앙정렬 */
  background: #4373f4;
  color: #fff;
  border-radius: 32px;
}

.two .content {
  border-top: 1px solid #ccc;
  margin: 0.5rem 0 0;
  padding: 1rem 0 0;
}
.two .swiper-button-next {
  color: #ccc;
}
.two .swiper-button-prev {
  color: #ccc;
}
</style>