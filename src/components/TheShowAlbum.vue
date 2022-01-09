<template>
  <div class="album-img">
    <img :src="album.artworkUrl100" alt="" />
  </div>
  <div class="album-info">
    <div class="album-name">Album Name: {{ album.collectionName }}</div>
    <div class="album-price">Price: {{ album.collectionPrice }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { ItunesResult } from "../types/ItunesTypes.interface";

export default defineComponent({
  props: {
    album: {
      type: Object as PropType<ItunesResult>,
      required: true
    }
  },
  setup() {
    return {};
  }
});
</script>

<style lang="scss">
.album{
  display: flex;
  align-items: center;
  margin-bottom: 50px;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 5px 20px #e3e3e3;
  &-img{
    width: 100px;
    margin-right: auto;
    img{
      width: 100px;
      height: 100px;
      object-fit: cover;
      border-radius: 50%;
      border: 3px solid #4dba87;
    }
  }
  &-info{
    width: calc(100% - 130px);
  }
  &-name{
    font-size: 1.2rem;
    font-weight: 700;
    margin-bottom: 0.7rem;
  }
}
</style>