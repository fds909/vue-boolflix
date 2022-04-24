<template>
    <div class="card">
        <img :src="`https://image.tmdb.org/t/p/w342${poster}`" alt="Poster">
        <div class="card-info">
            <h3>{{ title }}</h3>
            <div><strong>Original title: </strong>{{ originalTitle }}</div>
            <div>
                <strong>Language: </strong>
                <span v-if="flags.includes(language)">
                    <img class="flag-icon" :src="require(`../../assets/img/${language}.png`)" alt="Language Flag">
                </span>
                <span v-else>
                    <!-- Chiamata all'API nel caso la bandiera non fosse tra quelle nella cartella locale -->
                    <img class="flag-icon" :src="`https://countryflagsapi.com/png/${language}`" alt="Language Flag">
                </span>
            </div>
            <div class="vote">
                <div v-for="(star, index) in Math.ceil(vote / 2)" :key="index"><img src="../../assets/icons/star.svg" class="star-icon"></div>
                <div v-for="(star, index) in 5 - Math.ceil(vote / 2)" :key="index"><img src="../../assets/icons/star-empty.svg" class="star-icon"></div>
            </div>
        </div>
    </div>
</template>

<script>
import {library} from '@fortawesome/fontawesome-svg-core';
import {fas} from '@fortawesome/free-solid-svg-icons'

library.add(fas);

export default {
  name: 'CardComp',
  props: {
      title: String,
      originalTitle: String,
      language: String,
      vote: Number,
      poster: String
  },
  data() {
      return {
          flags: ['en', 'it', 'fr', 'es', 'de', 'ja', 'ko']
      }
  }
}
</script>

<style scoped lang="scss">
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css";

    .card {
        display: flex;
        flex-basis: calc(100% / 5);
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: black;
        color: white;
        border: 3px solid rgb(158, 0, 0);
        border-radius: 8px;
        position: relative;
    }

    .flag-icon {
        width: 30px;
    }

    .card-info {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
        width: 100%;
        opacity: 0;
        position: absolute;
        z-index: 10;
    }

    .card-info:hover {
        opacity: 1;
        background-color: black;
        transition: 0.5s;
    }

    img {
        max-width: 100%;
    }

    .vote {
        display: flex;
    }

    .star-icon {
        width: 20px;
    }

</style>