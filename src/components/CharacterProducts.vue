<template>
  <div>
    <div class="featured-comics">
      <div v-for="comic in comics" :key="comic.id">
      <router-link :to="{ name: 'comic', params: {id:comic.id} }">
      <ComicCard
        :comicPageUrl="'comics/'+comic.id"
        :key="comic.id"
        :image-url="comic.thumbnail.path + '.jpg'"
        :comicName="comic.title"
      /></router-link>
    </div>
    </div>
  </div>
</template>

<script>
import ComicCard from "@/components/ComicCard.vue";
import axios from "axios";
export default {
  components: {
    ComicCard,
  },
  name: "CharacterProducts",
  mounted() {
    this.getComics();
  },

  data() {
    return {
      comics: null,
    };
  },
  methods: {
    getComics() {
      axios
        .get(
          "https://gateway.marvel.com/v1/public/comics?limit=30&ts=100&apikey=9ba68562b5c70ba6442264f6c5add1c2&hash=cdf3beb7b14c2e38b26b3f2fdef6a2ee"
        )
        .then((response) => {
          this.comics = response.data.data.results;
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.featured-comics {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(15.82%,1fr));;
  align-items: center;
  justify-content: center;
  padding: 1.3rem;
  grid-gap: 30px;
  grid-template-rows: 6;
  min-width: 191px;
}
</style>
