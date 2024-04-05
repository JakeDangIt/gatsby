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