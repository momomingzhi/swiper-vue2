<template>
  <div>
    <div
      v-for="(item, listIndex) in cardList"
      v-if="index === listIndex"
      :key="listIndex"
      class="listCard"
    >
      {{ item.content }}
    </div>
  </div>
</template>

<script>
export default {
  name: "information",
  title: "Loop mode / Infinite loop",
  props: {
    index: Number,
  },
  created() {
    this.cardList = [
      {
        height: "2rem",
        content: "Image 98m",
      },
      {
        height: "4rem",
        content: "Image 108m",
      },
      {
        height: "6rem",
        content: "Image 123m",
      },
      {
        height: "8rem",
        content: "Image 152m",
      },
      {
        height: "10rem",
        content: "Image 176m",
      },
      {
        height: "10rem",
        content: "Image 200m",
      },
      {
        height: "10rem",
        content: "Image 230m",
      },
    ];
  },
  mounted() {
    const $menu = document.querySelectorAll(".listCard");
    this.cardList.forEach((item, _idx) => {
      $menu[_idx].style.height = item.height;
      // $menu[_idx].style.color = "red";
    });
  },
  data() {
    return {
      cardList: [],
    };
  },
};
</script>

<style>
.listCard {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 80%;
  background: #ddd;
  height: 20rem;
  margin: 0 auto;
}
</style>