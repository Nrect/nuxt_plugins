<template>
  <div id="app">
    <h1 class="h1">
      vue-lazy-youtube-video
    </h1>
    <p>
      Initially this component loads only a thumbnail of the video, but after being clicked it inserts
      <code>&lt;iframe&gt;&lt;/iframe&gt;</code> with
      <code>autoplay</code> attribute and appropriate
      <code>src</code> attribute. Thus we significantly
      decrease the page load size, serving the video to user when it's realy
      necessary.
    </p>
    <div class="videos">
      <ul class="videos__list">
        <li v-for="(video, index) in videos" :key="index" class="videos__item">
          <LazyYoutubeVideo
            :src="video.url"
            :preview-image-size="video.previewImageSize"
            :aspect-ratio="video.aspectRatio"
            :thumbnail-listeners="{ load: foo }"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import LazyYoutubeVideo from 'vue-lazy-youtube-video'

export default {
  name: 'App',
  components: {
    LazyYoutubeVideo
  },
  data () {
    return {
      videos: [
        {
          url: 'https://www.youtube.com/embed/TuYEpOjEU8w',
          previewImageSize: 'maxresdefault'
        },
        {
          url: 'https://www.youtube.com/embed/65MVwN_Kz1Q',
          previewImageSize: 'hqdefault'
        },
        {
          url: 'https://www.youtube.com/embed/KbX1gYtPVYE',
          previewImageSize: 'sddefault',
          aspectRatio: '1:1'
        },
        {
          url: 'https://www.youtube.com/embed/etKOc80-cw0',
          previewImageSize: 'mqdefault'
        }
      ]
    }
  },
  methods: {
    foo () {
      console.log('bar')
    }
  }
}
</script>

<style lang="scss">
  $gap: 20px;

  #app {
    font-family: sans-serif;
  }

  .h1 {
    text-align: center;
    color: #34495e;
  }

  p {
    text-align: center;
  }

  .videos {
    &__list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      padding-left: 0;
      margin: {
        top: 0;
        bottom: 0;
      }
      list-style: none;
    }

    &__item {
      width: calc(50% - #{$gap / 2});

      &:nth-child(n + 3) {
        margin-top: $gap;
      }
    }
  }
</style>
