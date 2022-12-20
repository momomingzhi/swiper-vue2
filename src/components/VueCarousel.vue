<template>
  <div class="listCard">
    <VueSlickCarousel v-bind="settings" ref="sliders">
      <div
        v-for="(item, index) in slidesWidth"
        :key="`${item.width}-${index}`"
        :style="{
          width: `${item.width}px`,
          border: '1px solid',
          overflow: 'auto',
        }"
      >
        <h1>{{ item.content }}</h1>
      </div>
    </VueSlickCarousel>
  </div>
</template>
 
<script>
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";

export default {
  name: "MyComponent",
  components: { VueSlickCarousel },
  props: {
    list: [],
  },
  mounted() {
    this.clientWidth = this?.$refs?.sliders?.$el?.clientWidth;
    const computedLen = this.slidesWidth.reduce(
      (acc, cur) => (acc += Number(cur.width)),
      0
    );
    this.slidesToShow = Math.round(this.clientWidth / computedLen);
    console.log("slidesToShow:", computedLen);
  },
  computed: {
    getClientWidth() {
      console.log("ㅎㅇㅎㅇ:", this?.$refs?.sliders);
      return this?.$refs?.sliders?.$el?.clientWidth;
    },
    slidesWidth() {
      const renderListLen = Math.floor(this.clientWidth / this.list.length);
      const { min, max } = { min: renderListLen, max: renderListLen + 50 };
      return this.list.map((item, idx) => {
        return {
          width: `${this.list[idx].length <= 3 ? min : max}`,
          content: this.list[idx],
        };
      });
    },
    settings() {
      return {
        dots: true,
        arrows: true,
        infinite: false,
        slidesToShow: this.slidesWidth.length,
        slidesToScroll: 2,
        variableWidth: true,
        resize: true,
        responsive: [
          {
            breakpoint: 400,
            settings: {
              slidesToShow: this.slidesWidth.length - 2,
            },
          },
          {
            breakpoint: 500,
            settings: {
              slidesToShow: this.slidesWidth.length,
            },
          },
          {
            breakpoint: 600,
            settings: {
              slidesToShow: this.slidesWidth.length,
            },
          },
          {
            breakpoint: 800,
            settings: {
              slidesToShow: this.slidesWidth.length,
            },
          },
          {
            breakpoint: 1024,
            settings: {
              slidesToShow: this.slidesWidth.length,
            },
          },
        ],
      };
    },
  },
  // watch: {
  //   "this?.$refs?.sliders?.$el?.clientWidth": {
  //     deep: true,
  //     immediate: true,
  //     handler(v) {
  //       console.log("$$", v);
  //     },
  //   },
  // },
  data() {
    return {
      renderArr: [],
      clientWidth: 0,
      slidesToShow: 1,
    };
  },
};
</script> 
<style>
* {
  background: mediumpurple;
}
.listCard {
  border: 1px solid;
  /* width: 90%; */
  margin: 0 auto 2rem auto;
}

.slick-dots {
  bottom: -30px !important;
}
</style>
