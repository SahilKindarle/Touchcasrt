<template>
  <q-page>
    <div class="container q-pl-lg" id="pageIdElement">
      <div class="row">
        <q-toolbar class="q-mt-md">
          <img src="src/assets/bmuse_logo.png" alt="" />
          <q-space></q-space>
          <q-btn round icon="search" class="q-mr-xs" color="black" />
        </q-toolbar>
        <div class="col-4 q-mt-xl">
          <div class="text-h1 text-white text-weight-thin">
            Bookshelf & <br />Book Racks
          </div>

          <div class="text-h5 text-white text-weight-thin">
            It is a long established fact that a reader will be distracted by
            the readable content of a page when looking at its layout. The point
            of using Lorem layout. The point of using Lorem
          </div>
        </div>
      </div>

      <div class="row q-mt-xl">
        <!-- {{ moviesData }} -->
        <!-- <div class="text-h5 text-white">Lorem Ipsum</div> -->
        <q-carousel
          v-model="slide"
          swipeable
          animated
          padding
          height="500px"
          class="bg-grey-1 shadow-2 rounded-borders"
          style="width: 400vw; background: transparent !important"
        >
          <q-carousel-slide :name="1" class="column no-wrap no-padding">
            <div
              class="row fit justify-start items-center q-gutter-xs q-col-gutter no-wrap"
            >
              <div v-for="(movie, index) in moviesData" :key="index">
                <!-- <div class="text-black">
                  {{ movie.title }}
                </div> -->
                <q-img
                  class="rounded-borders col-2 q-mx-md"
                  ratio="1"
                  height="500px"
                  width="300px"
                  style="border-radius: 50px"
                  :src="movie.book_image"
                  @click="setMovie(movie)"
                >
                  <div
                    class="absolute-bottom text-left text-h6"
                    style="background: rgba(0, 0, 0, 0.8)"
                  >
                    {{ movie.author }}
                    <br />
                    <span class="text-subtitle1">
                      {{ movie.publisher }}
                    </span>
                  </div>
                </q-img>
              </div>
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
    </div>
    <div class="bg-lightBlack">
      <div class="row bg-lightBlack" style="padding-top: 10%; padding-left: 8%">
        <div class="col-4">
          <div class="text-h3 text-blue text-weight-thin q-mb-xl">Lorem</div>
          <q-img
            :src="singleMovieData.book_image"
            height="auto"
            style="object-fit: scale-down; max-width: 20%"
          />
          <div class="text-h3 text-blue text-weight-thin q-mt-xl q-mb-xl">
            <q-btn
              color="grey-9"
              class="btn-fixed-width"
              icon-right="add"
              align="right"
              size="lg"
              no-caps
            >
              Add to Favorites
            </q-btn>
          </div>
        </div>
        <div class="col-8">
          <div class="text-h6 text-white text-weight-light">
            {{ singleMovieData.title }}
          </div>
          <div class="text-subtitle1 text-white text-weight-light q-mb-xl">
            {{ singleMovieData.author }}
          </div>
          <div class="text-white text-subtitle1 text-weight-light">
            <!-- Just gave multiple time to get the amopunt of data -->
            {{ singleMovieData.description }} {{ singleMovieData.description }}
            {{ singleMovieData.description }} {{ singleMovieData.description }}
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import axios from "src/boot/axios";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      slide: 1,
      moviesData: [],
      singleMovieData: {},
    };
  },
  mounted() {
    this.getMoviesData();
  },
  methods: {
    getMoviesData() {
      console.log("hello");
      this.$axios.get("src/assets/books.json").then((response) => {
        console.log(response.data.results.books);
        this.moviesData = response.data.results.books;
        this.singleMovieData = response.data.results.books[0];
      });
    },

    setMovie(movie) {
      this.singleMovieData = movie;
    },
  },
});
</script>

<style scoped>
#pageIdElement {
  background: url(../assets/bg.jpg) no-repeat center center;
  background-size: cover;
}

.btn-fixed-width {
  width: 300px;
}

.bg-lightBlack {
  background: #141517;
}

.q-layout__section--marginal {
  background: transparent;
}
</style>
