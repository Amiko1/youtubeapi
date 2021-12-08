<template>
  <div class="youtube">
    <input
      placeholder="find Video"
      class="youtube__input"
      type="text"
      v-model.lazy="videoName"
    />
    <div v-for="video in youtubeVideos" :key="video.id">
      <iframe
        class="youtube__player"
        width="560"
        height="315"
        :src="youtubeLink(video.id.videoId)"
        title="YouTube video player"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api: "https://www.googleapis.com/youtube/v3/search",
      videoName: "",
      youtubeVideos: [],
      Apikey: "AIzaSyAnnzTDzk1ASrSq7H2XT41p0dxulRk5ZOQ",
    };
  },
  methods: {
    async searchVideo(videoName) {
      const url = `${this.api}?key=${this.Apikey}&q=${videoName}&maxResults=5`;

      let data = await fetch(url);
      let videoData = await data.json();
      console.log(videoData);
      this.youtubeVideos = videoData.items;
      console.log(this.youtubeVideos);
    },
    youtubeLink(id) {
      return `https://www.youtube.com/embed/${id}`;
    },
  },
  watch: {
    videoName: function (value) {
      this.searchVideo(value);
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