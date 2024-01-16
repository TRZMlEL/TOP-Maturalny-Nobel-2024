<template class=" bg-gray-950">
  <div class=" bg-gray-950 flex flex-col gap-5 p-5 pr-64 pl-64">
    <div class="flex justify-between gap-5">
      <div class="text-white bg-emerald-800 rounded-2xl p-5 w-1/2 flex justify-between gap-5" v-if="jakub">
        <div class="w-2/3">
          <h2 class=" font-extrabold text-2xl">{{ jakub.name }}</h2>
          <p><span class="font-bold">{{ jakubIndex }}</span> miejsce</p>
          <p><span class="font-bold">{{ jakub.likes }}</span> like</p>
          <p><span class="font-bold">{{ jakub.views }}</span> wyświetleń</p>
          <p class="text-gray-300" v-if="jakubIndex > 1">Brakuje <span class="font-bold">{{ likesToNext }}</span> like do miejsca wyżej</p>
        </div>
        <button @click="goToMarkowskiVideo" class="bg-white text-gray-950 font-bold p-5 rounded-xl">Polub film <span class=" text-3xl">👍</span></button>
      </div>
      <div class="text-white bg-emerald-800 rounded-2xl p-5 w-1/2 text-center flex flex-col items-center justify-center">
        <h2>Do końca głosowania pozostało</h2>
        <p class="text-2xl font-semibold">{{ days }} dni, {{ hours }} godzin, {{ minutes }} minut, {{ seconds }} sekund</p>
      </div>
    </div>

    <div v-for="(video, index) in sortedVideos" :key="index" :class="{' bg-emerald-600': index < 20, 'bg-emerald-800': index >= 20, 'rounded-2xl': true, 'text-white': true, 'p-5': true}">
      <h2 class="text-lg"><span class="font-bold">{{ index + 1 }} miejsce</span> - {{ video.name }}</h2>
      <p>Like: <span class="font-semibold">{{ video.likes }}</span></p>
      <p>Wyświetleń: <span class="font-semibold">{{ video.views }}</span></p>
      <!-- <p v-if="index !== 0">{{ sortedVideos[index - 1].likes - video.likes }} do miejsca {{ index }}</p> -->
    </div>
  </div>
</template>

<script setup>
  import { ref, computed, onMounted, onUnmounted } from 'vue';

  //----Przekierowanie do Filmu Markowskiego
  const goToMarkowskiVideo = () => {
    window.location = 'https://www.youtube.com/watch?v=JVle6J4QAWU'
  }

  // ----Odliczanie
  const targetDate = new Date('2024-01-31T00:00:00+01:00');
  const days = ref(0);
  const hours = ref(0);
  const minutes = ref(0);
  const seconds = ref(0);

  function updateCountdown() {
    const now = new Date();
    const totalSeconds = (targetDate - now) / 1000;

    days.value = Math.floor(totalSeconds / 3600 / 24);
    hours.value = Math.floor(totalSeconds / 3600) % 24;
    minutes.value = Math.floor(totalSeconds / 60) % 60;
    seconds.value = Math.floor(totalSeconds % 60);
  }

  let intervalId;

  onMounted(() => {
    updateCountdown();
    intervalId = setInterval(updateCountdown, 1000);
  });

  onUnmounted(() => {
    clearInterval(intervalId);
  });

  //------API

  const videos = ref([
    { id: 'JVle6J4QAWU', name: 'Jakub Markowski', likes: 0, views: 0 },
    { id: 'zoqbUp_EY0A', name: 'Kornelia Wieczorek', likes: 0, views: 0 },
    { id: 'v2PIexmuvck', name: 'Jan Wesołek', likes: 0, views: 0 },
    { id: 'yNbDW2DWIkk', name: 'Piotr Turlejski', likes: 0, views: 0 },
    { id: 'q4mLr7mWuJA', name: 'Marcelina Marciniak', likes: 0, views: 0 },
    { id: 'mcuYkTy31dw', name: 'Marcelina Maciąg', likes: 0, views: 0 },
    { id: 'rH4qekHJlaA', name: 'Oliwia Łubińska', likes: 0, views: 0 },
    { id: 'r3W2ephpPCE', name: 'Diana Serjant', likes: 0, views: 0 },
    { id: 'j_i0xZ1g7k0', name: 'Matylda Baradziej', likes: 0, views: 0 },
    { id: 'io7Z23paGmg', name: 'Mateusz Gwiazda', likes: 0, views: 0 },
    { id: 'lRBB182ChPI', name: 'Julia Żugaj', likes: 0, views: 0 },
    { id: 'yiDSBhpFYTc', name: 'Wiktor Chmielarz', likes: 0, views: 0 },
    { id: 'vvuiNtaJVD8', name: 'Mikołaj Napieralski', likes: 0, views: 0 },
    { id: 'eS9cFz_6XQ0', name: 'Karolina Wenta', likes: 0, views: 0 },
    { id: 'Vqa2zRlNOpo', name: 'Laura Brzeska', likes: 0, views: 0 },
    { id: 'ovIgL98ngz0', name: 'Kaja Możdżeń', likes: 0, views: 0 },
    { id: 'xgO4EVJlAUY', name: 'Maja Wieleba', likes: 0, views: 0 },
    { id: 'wPUcCTWjbQs', name: 'Agata Jacaszek', likes: 0, views: 0 },
    { id: 'wEQv-g0g2Us', name: 'Patryk Stelmaszek', likes: 0, views: 0 },
    { id: 't-2pYLgWC5Y', name: 'Kacper Czerwiński', likes: 0, views: 0 },
    { id: 'qAzksNVh364', name: 'Julia Wierzgała', likes: 0, views: 0 },
    { id: '_Mt1fH6LsY4', name: 'Bartosz Sułkowski', likes: 0, views: 0 },
    { id: 'yuCtTspWMas', name: 'Michał Łukasiak', likes: 0, views: 0 },
    { id: 'k6UbdFdpfd0', name: 'Damian Zioło', likes: 0, views: 0 },
    { id: 'VY47Tuw9I9I', name: 'Dawid Rzitka', likes: 0, views: 0 },
    { id: 'rTs1IsTDO1o', name: 'Monika Golon', likes: 0, views: 0 },
    { id: 'pgJub8rZnO8', name: 'Norbert Mazur', likes: 0, views: 0 },
    { id: 'VS_8J7jqERw', name: 'Zuzanna Folek', likes: 0, views: 0 },
    { id: 'PP-7kwHnLtU', name: 'Gabriela Kutyma', likes: 0, views: 0 },
    { id: 'jjh8wE0ciL0', name: 'Sylwester Starczewski', likes: 0, views: 0 },
    { id: 'ffHRnxJE7qE', name: 'Pola Kosicka', likes: 0, views: 0 },
    { id: 'iSe9MyWZ_cM', name: 'Antonina Janczyk', likes: 0, views: 0 },
    { id: '_3AKbRBtbM8', name: 'Helena Góralczyk', likes: 0, views: 0 },
    { id: 'WZ8Eb2RsnRc', name: 'Lena Jurczuk', likes: 0, views: 0 },
    { id: 'dPEQVFwyBqg', name: 'Mateusz Król', likes: 0, views: 0 },
    { id: 'cg4NJPRb_HE', name: 'Bartosz Bilski', likes: 0, views: 0 },
    { id: 'cZUlSpq6AOg', name: 'Zofia Pielorz', likes: 0, views: 0 },
    { id: 'YcOGHSfTNS8', name: 'Tymoteusz Sobczak', likes: 0, views: 0 },
    { id: 'WpJk8I8an4I', name: 'Kacper Kupczak', likes: 0, views: 0 },
    { id: 'TwD-q4fvfZo', name: 'Bartosz Kucia', likes: 0, views: 0 },
    { id: 'MBXEPIZwpm8', name: 'Natalia Frątczak', likes: 0, views: 0 },
    { id: 'QkhqaytQEcg', name: 'Aleksandra Ryk', likes: 0, views: 0 },
    { id: 'GYBSkAsraYg', name: 'Nikodem Biniecki', likes: 0, views: 0 },
    { id: 'U4-HYcw1NYM', name: 'Patrycja Zdyb', likes: 0, views: 0 },
    { id: 'HMCpxqYKfd8', name: 'Łukasz Winkler', likes: 0, views: 0 },
    { id: 'PUlj0GkLQAs', name: 'Zuzanna Kosieradzka', likes: 0, views: 0 },
    { id: 'Q6LvclSDwg0', name: 'Joanna Tokarz', likes: 0, views: 0 },
    { id: 'Efh3W_O2K6Q', name: 'Oliwier Chomicz', likes: 0, views: 0 },
    { id: 'DbC1-Tswvi4', name: 'Tatiana Werner', likes: 0, views: 0 },
    { id: 'QOHgSCXuRsU', name: 'Zuzanna Patulska', likes: 0, views: 0 },
    { id: 'MInZIX2wTqk', name: 'Wojciech Wasilewski', likes: 0, views: 0 },
    { id: 'L0Ff8rE8D8o', name: 'Olga Duchnik', likes: 0, views: 0 },
    { id: 'D6uMeAZc5DQ', name: 'Mateusz Łojewski', likes: 0, views: 0 },
    { id: 'GB4iLrrovb8', name: 'Kamil Banasik', likes: 0, views: 0 },
    { id: '8_5I8yNX6VY', name: 'Michalina Pyrek', likes: 0, views: 0 },
    { id: '6sbhMHEXpr4', name: 'Kuba Szpila', likes: 0, views: 0 },
    { id: '3Y61a3YRY9I', name: 'Maciej Pytka', likes: 0, views: 0 },
    { id: '85XY6VpMeJU', name: 'Dominika Szostek', likes: 0, views: 0 },
    { id: '5NPSIfdl-dk', name: 'Marta Łopka', likes: 0, views: 0 },
    { id: 'a2EpD8cO5H4', name: 'Zuzanna Marzejon', likes: 0, views: 0 },
    { id: '4ga_HM5a7PY', name: 'Paweł Wojdyła', likes: 0, views: 0 },
    { id: '1N2QJGbsJJU', name: 'Paulina Kudzia', likes: 0, views: 0 },
    { id: '-qfOWL0HPVg', name: 'Hanna Mielke', likes: 0, views: 0 },
    { id: '-_fCbUnNnZM', name: 'Piotr Kostrzewa', likes: 0, views: 0 },
    { id: 'M8fozu1vSYA', name: 'Anita Bałuka', likes: 0, views: 0 },
    { id: 'hvngW1dVTp0', name: 'Ada Świerżewska', likes: 0, views: 0 },
  ]);

  async function getVideoLikes(video) {
    const apiKey = 'AIzaSyBbRZVHZTV7dVFl_MSeJ-NQcKtDqzqaOZ0'; // Twój klucz API YouTube
    const url = `https://www.googleapis.com/youtube/v3/videos?part=statistics&id=${video.id}&key=${apiKey}`;

    try {
      const response = await axios.get(url);
      video.likes = response.data.items[0].statistics.likeCount;
      video.views = response.data.items[0].statistics.viewCount;
      console.log(`${video.name} ma ${video.likes} polubień.`);
    } catch (error) {
      console.error(error);
    }
  }

  Promise.all(videos.value.map(getVideoLikes)).then(() => {
    // Sortuj filmy od największej do najmniejszej liczby polubień
    videos.value.sort((a, b) => b.likes - a.likes);
  });

  const sortedVideos = computed(() => videos.value.sort((a, b) => b.likes - a.likes));

  const jakub = computed(() => videos.value.find(video => video.name === 'Jakub Markowski'));
  const jakubIndex = computed(() => videos.value.findIndex(video => video.name === 'Jakub Markowski') + 1);
  const likesToNext = computed(() => {
    if (jakubIndex.value > 1) {
      return videos.value[jakubIndex.value - 2].likes - jakub.value.likes;
    }
    return 0;
  });
</script>
