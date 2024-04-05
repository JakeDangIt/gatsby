<template>
  <div class="flex w-screen h-screen justify-center">
    <AudioPlayer
      v-for="song in playlist"
      :key="song.id"
      :src="song.src"
      :albumCover="song.albumCover"
      :songTitle="song.songTitle"
      :artist="song.artist"
      :bgPicture="song.bgPicture"
      :gatsbyExplanation="song.gatsbyExplanation"
      :songLink="song.songLink"
      :setting="song.setting"
      :class="{ hidden: selectedSongIndex !== song.id }"
      @playNext="playNext"
      @playPrevious="playPrevious"
    />
  </div>
  <div class="playlist">
    <ul 
        class="fixed bottom-5 right-20 px-2 rounded-lg bg-stone-400 list-decimal">
      <li
        v-for="song in playlist"
        :key="song.id"
        @click="selectedSongIndex = song.id"
        class="cursor-pointer ml-10 p-2 hover:bg-stone-300 rounded-lg"
        :class="{ 'font-bold': selectedSongIndex === song.id }"
      >
        {{ song.songTitle }} - {{ song.artist }}
      </li>
    </ul>
  </div>
  <div class="github-link">
    <a href="https://github.com/JakeDangIt/gatsby/tree/main/gatsby-music">
      <img src="./assets/GitHub_Invertocat_Logo.svg.png" alt="" class="fixed h-10 bottom-0 left-0 invert">
    </a>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import AudioPlayer from './components/AudioPlayer.vue';
import playlist from '../playlist';

const selectedSongIndex = ref(0);

function playNext() {
  // if the current song is the last song in the playlist, wrap around to the first song
  selectedSongIndex.value = selectedSongIndex.value === playlist.length - 1 ? 0 : selectedSongIndex.value + 1;
}

function playPrevious() {
  // if the current song is the first song in the playlist, wrap around to the last song
  selectedSongIndex.value = selectedSongIndex.value === 0 ? playlist.length - 1 : selectedSongIndex.value - 1;
}
</script>

<style scoped>
/* Add your CSS styles here */
</style>