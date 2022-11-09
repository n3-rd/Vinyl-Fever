<template>
  <div class="text-[3rem] font-black px-11 py-11">Vinyl on sale</div>
  <div class="w-screen md:px-12">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 w-full">
      <div
        v-for="vinyl in vinyls"
        :key="vinyl.id"
        class="vinyl-sale-container h-[25rem] w-full bg-black flex justify-end items-end bg-cover bg-center"
        :style="{ backgroundImage: `url(${vinyl.image})` }"
      >
        <div
          class="vinyl-sale-overlay h-[10rem] w-full bg-black flex justify-center items-center"
        >
          <div
            class="vinyl-sale-title text-white text-[2rem] font-black capitalize"
          >
            {{ vinyl.title }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "VinylSale",
  data() {
    return {
      vinyls: [
        {
          id: 1,
          title: "King Gizzard & The Lizard Wizard",
          image: "/img/1.jpg",
        },
        {
          id: 2,
          title: "Freddie Gibbs & Madlib",
          image: "/img/2.jpg",
        },
        {
          id: 3,
          title: "The Avalanches",
          image: "/img/3.jpg",
        },
        {
          id: 4,
          title: "Gorillaz",
          image: "/img/4.jpg",
        },
        {
          id: 5,
          title: "Washed Out",
          image: "/img/2.jpg",
        },
        {
          id: 6,
          title: "Sufjan Stevens",
          image: "/img/1.jpg",
        },
        {
          id: 7,
          title: "30 Seconds To Mars",
          image: "/img/4.jpg",
        },
        {
          id: 8,
          title: "queens of the stone age",
          image: "/img/3.jpg",
        },
      ],
    };
  },
};
</script>
