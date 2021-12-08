<template>
  <div class="youtube">
    <input
      placeholder="find Video"
      class="youtube__input"
      type="text"
      v-model="videoName"
    />
    <button class="youtube__button" @click="searchVideo">SEARCH</button>
    <iframe
      class="youtube__player"
      width="560"
      height="315"
      :src="youtubeLink"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    ></iframe>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api: "https://www.googleapis.com/youtube/v3/search",
      videoName: "",
      videoId: "",
      key: "AIzaSyB8OKTW0EC_taAgJSyi7pg2fyFftPVVum8",
    };
  },
  methods: {
    async searchVideo() {
      const url = `${this.api}?key=${this.key}&q=${this.videoName}&part=snippet&maxResults=1`;
      let data = await fetch(url);

      let videoData = await data.json();
      this.videoId = videoData.items[0].id.videoId;
    },
  },
  computed: {
    youtubeLink() {
      return `https://www.youtube.com/embed/${this.videoId}`;
    },
  },
};
</script>

<style>
.youtube {
  padding-top: 5em;
  width: 30%;
  min-width: 550px;
  margin: auto;
  display: flex;
  gap: 2em;
  flex-direction: column;
}

.youtube__input {
  padding: 1em;
  border-bottom: 1px solid black;
  outline: none;
}

.youtube__button {
  padding: 1em;
  background-color: brown;
  cursor: pointer;
}

.youtube__button:hover {
  opacity: 0.7;
}

.youtube__player {
  width: 100%;
}
</style>
