<template>
  <header>
    <nav v-if="!authenticationStore.loadingSession">
        <router-link :to="{name:'newComic'}" v-if="authenticationStore.userData">Add new comic</router-link>
        <router-link :to="{name:'comic-collection'}">Comic collection</router-link>

    </nav>
    <div v-else>
      Loading...
    </div>

  </header>
  <input
            class="input filter"
            @change="filter"
            v-model="filterContain"
          />
  <main><Comic/></main>
</template>

<script>
import Comic from '../components/Comic.vue';
import { useComicsStore } from '../stores/comics';
import { mapStores } from "pinia";
import {useAuthenticationStore} from '../stores/authentication';
//import { db } from '@/firebase';

export default {
    components:{
      Comic
    },
    computed:{
      ...mapStores(useAuthenticationStore),
      ... mapStores(useComicsStore)
    }

}
</script>

<style>
  body{
    width: 100%;
  height: 100vh; /* 100% of the viewport height */
  margin: 0;
  }
    main{
    margin: 0;
    padding: 0;
  }
    nav{
        background-color: #D9F0FF;
        display:flex;
        justify-content:space-around
    }
    
    main{
      background-image: linear-gradient(rgba(153, 123, 123, 0.5), rgba(136, 41, 41, 0.5)), url('../assets/HorizonteCalm.jpg');
      background-size: cover;
      background-position: bottom;
      transition : 0.4s;
    }

</style>