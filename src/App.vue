<template>
  <form class="search-form" @submit.prevent="searchItunes(searchText)">
    <input class="search-form__input" type="text" v-model="searchText" />
    <button class="search-form__btn" @click="searchItunes(searchText)">Search</button>
  </form>
  <div v-if="data.results">
    <div class="album" v-for="album in data.results" :key="album.artistId">
      <Album :album="album" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from "vue";
import { itunesSearch } from "./services/iTunesAPI";
import { ItunesTypes } from "./types/ItunesTypes.interface";
import Album from "./components/Album.vue";

export default defineComponent({
  name: "App",
  components: {
    Album
  },
  setup() {
    let albums = reactive<{ data: ItunesTypes }>({ data: {} });
    let searchText = ref("");
    const searchItunes = async (search: string): Promise<void> => {
      const value = await itunesSearch(search);
      albums.data = value;
    };

    return { searchItunes, ...toRefs(albums), searchText };
  }
});
</script>

<style lang="scss">
body{
  margin: 0;
  padding: 0;
}
*{
  box-sizing: border-box;
  font-family: sans-serif;
}
#app{
  max-width: 600px;
  margin: 100px auto 0;
}
.search-form{
  display: flex;
  justify-content: space-between;
  margin-bottom: 30px;
  &__input{
    width: calc(100% - 85px);
    padding: 0 12px;
    border: 1px solid #4dba87;
    border-radius: 5px;
    &:focus{
      outline: none;
    }
  }
  &__btn{
    padding: 10px 16px;
    border-radius: 5px;
    color: #fff;
    border: 0;
    background: #4dba87;
  }
}
</style>
