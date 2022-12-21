<template>
  <div class="listCard">
    <VueSlickCarousel v-bind="settings" ref="sliders">
      <div
        v-for="(item, index) in slidesWidth"
        :key="`${item.width}-${index}`"
        :style="{
          width: `${item.width}px`,
          border: '1px solid #fff',
          background: '#00a52a',
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
    this.slidesToShow = Math.ceil(computedLen / this.clientWidth);
    console.log(
      "slidesToShow:",
      this.clientWidth,
      computedLen,
      this.slidesToShow
    );
  },
  computed: {
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
        // slidesToShow: this.slidesWidth.length,
        // slidesToScroll: this.slidesWidth.length - this.slidesToShow,
        variableWidth: true,
        resize: true,
        responsive: [
          {
            breakpoint: 400,
            settings: {
              slidesToShow: this.slidesWidth.length - this.slidesToShow,
            },
          },
          {
            breakpoint: 500,
            settings: {
              slidesToShow: this.slidesWidth.length - this.slidesToShow,
              // slidesToScroll: 4,
            },
          },
          {
            breakpoint: 600,
            settings: {
              slidesToShow: this.slidesWidth.length - this.slidesToShow,
            },
          },
          {
            breakpoint: 800,
            settings: {
              slidesToShow: this.slidesWidth.length - this.slidesToShow,
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
button.slick-prev:before,
button.slick-next:before {
  background-color: #ccc !important;
}
.listCard {
  width: 90%;
  margin: 0 auto 2rem auto;
  background: #fe987b !important;
}
</style>
