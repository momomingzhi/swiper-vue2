
<template>
  <section class="two">
    <swiper
      class="swiper2"
      :options="swiperOption2"
      @click-slide="clickSlide"
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
      class="swiper"
      :options="swiperOption"
      ref="mySwiper"
      @slideChange="slideChange"
    >
      <!-- <div class="top-menu"> -->
      <swiper-slide v-for="(slideContent, index) in list" :key="index">
        {{ slideContent }}
        <component :is="dynamicComponent" v-bind:index="index"></component>
      </swiper-slide>
      <!-- </div> -->

      <!-- <swiper-slide
        v-for="(slideContent, index) in list"
        :key="index"
        :class="[isActive === index ? 'active' : '']"
      >
        <component :is="dynamicComponent" v-bind:index="index"></component>
      </swiper-slide> -->

      <!-- <div class="swiper-pagination" slot="pagination"></div> -->
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
    this.list = ["98m", "108m", "123m", "152m", "176m"];
  },
  computed: {
    swiper() {
      console.log("swiper computed");
      return this.$refs.mySwiper.$swiper;
    },
    menuSwiper() {
      return this.$refs.menuSwiper.$swiper;
    },
  },
  mounted() {
    //console.log('Current Swiper instance object', this.swiper)
    //this.menuSwiper.slideTo(5, 1000, false);
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
        loop: false,
        on: {
          click: function () {
            console.log("밑에 카드 클릭!!!!!");
          },
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
      swiperOption2: {
        slidesPerView: 4,
        spaceBetween: 10,
        slidesPerGroup: 2,
        loop: false,
        on: {
          init: function () {
            console.log("menu init");
          },
          click: function () {
            //console.log("menu 클릭!!!!!", this);
            // this.swiper.slideTo(this.menuSwiper.activeIndex, 1000, false);
          },
          slideChange: function (data) {
            console.log("menu slide Change", this);
          },
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
    };
  },

  methods: {
    clickSlide(index, reallyIndex) {
      console.log("dddddddd", index);
      // const emptyArr = Array.from({ length: index - 1 }, () => 1);
      // this.list.push(...emptyArr);
      //this.menuSwiper.appendSlide(`<div class="swiper-slide">new new</div>`);
      // this.swiper.slideTo(this.menuSwiper.activeIndex, 1000, false);
      //this.swiper.slideTo(index, 1000, false);
      this.menuSwiper.slideNext();

      console.log("나옴");
      //this.menuSwiper.removeSlide(this.list.length - 1);
      //this.isActlive = index;
      //this.menuSwiper.slideTo(3, 1000, false);
    },
    clickNavigation(index) {
      //console.log("dddddd", this._this);
    },

    slideChange() {
      // console.log("이거:", this.swiper.activeIndex);
      //this.isActive = this.swiper.activeIndex;
      //this.menuSwiper.slideTo(this.swiper.activeIndex, 1000, false);
      // console.log(
      //   "isActive:",
      //   this.isActive,
      //   this.swiper.activeIndex,
      //   this.menuSwiper.activeIndex
      // );
    },
  },
};
</script>

<style>
.two {
  margin: 3rem 0 0;
}
.swiper2 .swiper-slide {
  /* display: flex; */
  /* flex-direction: column; */
  border: 1px solid;
}

.top-menu {
  display: flex;
  background: chartreuse;
  height: 100%;
  /* cursor: pointer; */
}
.two .active {
  /* background: #4373f4; */
  /* color: #fff; */
  /* border-radius: 32px; */
}
.two .swiper-button-next {
  color: #ccc;
}
.two .swiper-button-prev {
  color: #ccc;
}
</style>