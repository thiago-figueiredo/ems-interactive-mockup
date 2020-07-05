<template>
  <div>
    <button
      class="media-item"
      v-on:keydown.enter="action('photoCount')"
      @click="action('photoCount')"
    >
      <img class="media-item-icon" src="../assets/photo-camera.svg" />
      <span>Photo</span><span class="media-item-counter">{{ photoCount }}</span>
    </button>
    <button
      class="media-item"
      v-on:keydown.enter="action('idCount')"
      @click="action('idCount')"
    >
      <img class="media-item-icon" src="../assets/id-card.svg" />
      <span>ID</span><span class="media-item-counter">{{ idCount }}</span>
    </button>
    <button
      class="media-item"
      v-on:keydown.enter="action('ekgCount')"
      @click="action('ekgCount')"
    >
      <img class="media-item-icon" src="../assets/like.svg" />
      <span>EKG</span><span class="media-item-counter">{{ ekgCount }}</span>
    </button>
    <button
      class="media-item"
      v-on:keydown.enter="action('videoCount')"
      @click="action('videoCount')"
    >
      <img class="media-item-icon" src="../assets/video-camera.svg" />
      <span>Video</span><span class="media-item-counter">{{ videoCount }}</span>
    </button>
    <button
      class="media-item"
      v-on:keydown.enter="action('voiceMemoCount')"
      @click="action('voiceMemoCount')"
    >
      <img class="media-item-icon" src="../assets/microphone.svg" />
      <span>Voice Memo</span
      ><span class="media-item-counter">{{ voiceMemoCount }}</span>
    </button>
    <button
      class="media-item"
      v-on:keydown.enter="action('liveConsultCount')"
      @click="action('liveConsultCount')"
    >
      <img class="media-item-icon" src="../assets/video-camera.svg" />
      <span>Live Consult</span
      ><span class="media-item-counter">{{ liveConsultCount }}</span>
    </button>
  </div>
</template>

<script>
export default {
  name: "media",

  data() {
    return {
      ekgCount: 0,
      idCount: 0,
      liveConsultCount: 0,
      photoCount: 0,
      videoCount: 0,
      voiceMemoCount: 0,
    };
  },

  methods: {
    action(type) {
      this[type] += 1;
    },
  },
};
</script>

<style scoped>
.media-item {
  align-items: center;
  background-color: var(--nc-bg-1);
  border: 1px solid var(--nc-tx-2);
  display: flex;
  font-size: 1.2rem;
  margin-bottom: 0.2rem;
  padding: 1rem;
  transition: background-color 0.2s;
  width: calc(100% - 1px);
}

.media-item:hover {
  background-color: var(--nc-bg-2);
  outline: none;
}

.media-item:focus {
  background-color: var(--nc-bg-3);
  outline: none;
}

.media-item-counter {
  border: 1px solid white;
  border-radius: 4px;
  display: inline-block;
  margin-left: auto;
  text-align: center;
  width: 26px;
}

.media-item-icon {
  height: 35px;
  margin-bottom: 0;
  padding-right: 1rem;
}
</style>
