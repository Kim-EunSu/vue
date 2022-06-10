<template>
  <HeaderCont />
  <main id="main">
    <section class="movie__cont">
      <TitleCont name1="Movie" name2="reference" />
      <div class="container">
        <div class="movie__inner">
          <div class="movie__top">
            <div class="title">Top10 콘텐츠</div>
            <swiper
              :slides-per-view="3"
              :space-between="50"
              :centeredSlides="true"
              :pagination="{
                clickable: true,
              }"
              :modules="modules"
              class="mySwiper"
              @swiper="onSwiper"
              @slideChange="onSlideChange"
            >
              <swiper-slide
                v-for="(topmovie, index) in topmovies"
                :key="topmovie.id"
              >
                <img
                  :src="
                    'https://image.tmdb.org/t/p/w500/' + topmovie.poster_path
                  "
                  :alt="topmovie.title"
                />
                <div class="movie_num">{{ index + 1 }}</div>
                <!-- <span class="title">{{ topmovie.title }}</span> -->
              </swiper-slide>
              <!-- <swiper-slide>Slide 2</swiper-slide>
              <swiper-slide>Slide 3</swiper-slide> -->
            </swiper>
          </div>
          <div class="movie__search">
            <form @submit.prevent="SearchMovies()">
              <label for="search" class="sr-only">검색하기</label>
              <input
                type="search"
                id="search"
                placeholder="검색하기"
                v-model="search"
              />
              <button type="submit">검색</button>
            </form>
          </div>
          <div class="movie__list" v-if="movies.length !== 0">
            <ul>
              <li v-for="movie in movies" :key="movie.id">
                <img
                  v-if="movie.poster_path"
                  :src="'https:image.tmdb.org/t/p/w500/' + movie.poster_path"
                  alt="movie.title"
                />
                <img v-else src="../assets/img/nullimage.jpg" alt="" />
                <span class="title">{{ movie.title }}</span>
              </li>
            </ul>
          </div>
          <div class="noresult" v-else>검색결과가 없습니다.</div>
        </div>
      </div>
      <ContactCont />
    </section>
  </main>
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";
// Import Swiper styles
import "swiper/css";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const movies = ref([]);
    //매개변수설정
    const topmovies = ref([]);

    const search = ref("spiderman");
    const onSwiper = (swiper) => {
      console.log(swiper);
    };
    const onSlideChange = () => {
      console.log("slide change");
    };

    const Topmovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch(
        "https://api.themoviedb.org/3/movie/top_rated?api_key=c0567696bc620eac81b5e3baab58ee88&language=en-US&page=1",
        requestOptions
      )
        .then((response) => response.json())
        .then((data2) => {
          topmovies.value = data2.results;
          console.log(data2);
        })
        .catch((error) => console.log("error", error));
    };
    Topmovies();

    const SearchMovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=9278d13f704ad0fe53c2263b692efd89&query=${search.value}`,
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => {
          movies.value = data.results;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
    };
    SearchMovies();

    return {
      movies,
      topmovies,
      search,
      SearchMovies,
      onSwiper,
      onSlideChange,
    };
  },
};
</script>

<style lang="scss" scoped>
.title {
  color: #444;
  font-size: 70px;
}
.movie__top {
  margin-bottom: 10%;

  .swiper {
    width: 100%;
    height: 100%;
  }

  .swiper-slide {
    /* Center slide text vertically */
    display: -webkit-box;
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    -webkit-justify-content: center;
    justify-content: center;
    -webkit-box-align: center;
    -ms-flex-align: center;
    -webkit-align-items: center;
    align-items: center;
  }

  .movie_num {
    position: absolute;
    left: 0%;
    top: 0%;
    color: #f0eeeb;
    font-size: 200px;
    font-weight: 900;
    -webkit-text-stroke: 8px #444;
    z-index: 10;
  }

  .swiper-slide img {
    display: block;
    width: 70%;
    height: 100%;
    object-fit: cover;
    .title {
      font-family: var(--subKor_font);
      font-size: 4vw;
      margin-bottom: 20px;
    }
  }
}
.swiper-slide {
  padding-top: 130px;
  img {
    position: relative;
    z-index: 10;
  }
}

.movie__search {
  position: relative;

  input {
    border: 2px solid var(--light_border);
    width: 100%;
    background: var(--black);
    border-radius: 50px;
    padding: 1rem 3rem 1rem 2rem;
    color: var(--light_bg);
    font-family: var(--subKor_font);
    margin-bottom: 3%;
  }
  button {
    position: absolute;
    right: 10px;
    top: 9px;
    background: transparent;
    border: 0;
    color: var(--black);
    background: var(--white);
    font-family: var(--subKor_font);
    width: 40px;
    height: 40px;
    border-radius: 50%;
    font-size: 12px;
    transition: opacity 0.3 ease;

    &:active {
      opacity: 0.7;
    }
  }
}
.movie__cont {
  background: var(--dark_bg);
}
.movie__list {
  ul {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 1%;

    li {
      width: 24%;

      .title {
        font-size: 16px;
        font-family: var(—subKor_font);
        display: block;
        padding: 2% 0;
        margin-bottom: 3%;
      }
    }
  }
}
.noresult {
  font-size: 2vw;
  text-align: center;
}
</style>
