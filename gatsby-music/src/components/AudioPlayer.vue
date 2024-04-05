<template>
  <div
    v-if="audioReady"
    class="audio-player w-screen flex flex-row justify-center items-center"
    :style="{ backgroundImage: 'url(' + bgPicture + ')' }"
  >
    <div class="album-cover w-1/5 ml-40 mr-10">
      <img :src="albumCover" alt="Album Cover" class="rounded-2xl" draggable="false" />
    </div>

    <div class="flex flex-col">
      <div class="song-info bg-stone-600 p-4 rounded-xl my-2 border-2 border-white">
        <a :href="songLink" target="_blank" class="font-bold underline text-xl">{{ songTitle }}</a>
        <p>{{ artist }}</p>
      </div>

      <div class="controls flex gap-2 items-center bg-stone-500 border-2 border-cyan-500 p-2 rounded-lg">
        <button class="text-xl" @click="pausePlay">⏯️</button>
        <input type="range" class="seek-slider" @input="seek" :max="audio.duration" :value="audio.currentTime">
        <span>{{ formatTime(currentTime) }} / {{ formatTime(audio.duration) }}</span>
      </div>

      <div class="sidebar fixed left-20 top-20 bg-stone-600 p-4 w-1/5 h-4/5 rounded-xl">
        <h2 class="font-bold text-3xl">{{ setting }}</h2>
        <p>{{ gatsbyExplanation }}</p>
      </div>

      <div class="controls flex m-2 gap-4">
        <button @click="playPrevious" class="bg-white p-2 rounded-lg">Previous</button>
        <button @click="playNext" class="bg-white p-3 rounded-lg">Next</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const props = defineProps({
  src: String,
  albumCover: String,
  songTitle: String,
  artist: String,
  gatsbyExplanation: String,
  bgPicture: String,
  songLink: String,
    setting: String,
})
const emit = defineEmits(['playNext', 'playPrevious'])

const audio = new Audio(props.src)
const currentTime = ref(0);
const audioReady = ref(false);

function pausePlay() {
  if (audio.paused) {
    audio.play()
  } else {
    audio.pause()
  }
}

function playNext() {
    if (!audio.paused) {
        audio.pause()
    }
  emit('playNext')
}
function playPrevious() {
    if (!audio.paused) {
        audio.pause()
    }
  emit('playPrevious')
}
function seek(event) {
  audio.currentTime = event.target.value;
}

function formatTime(time) {
  const minutes = Math.floor(time / 60);
  const seconds = Math.floor(time % 60);
  return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
}


audio.addEventListener('canplay', () => {
  audioReady.value = true;
});

audio.addEventListener('timeupdate', () => {
  currentTime.value = audio.currentTime;
});
</script>

<style scoped>
h2,
h3,
a,
p {
  color: white;
}
.audio-player {
  background-size: cover;
  background-position: center;
}
</style>
