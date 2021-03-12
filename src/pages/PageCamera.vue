<template>
  <q-page class="constrain-more q-pa-md">
    <div class="camera-frame q-pa-md">
      <video class="full-width" autoplay ref="video" />
    </div>
    <div class="text-center q-pa-md">
      <q-btn round color="grey-10" icon="eva-camera" size="lg" />
    </div>
    <div class="row justify-center q-ma-md">
      <q-input
        class="col col-sm-6"
        v-model="post.caption"
        label="Caption"
        dense
      />
    </div>
    <div class="row justify-center q-ma-md">
      <q-input
        class="col col-sm-6"
        v-model="post.location"
        label="Location"
        dense
      >
        <template v-slot:append>
          <q-btn round dense flat icon="eva-navigation-2-outline" />
        </template>
      </q-input>
    </div>
    <div class="row justify-center q-ma-md">
      <q-btn unelevated rounded label="Post Image" color="primary" />
    </div>
  </q-page>
</template>

<script>
import { uid } from "quasar";
// require("md-gum-polyfill");

export default {
  name: "PageCamera",
  data() {
    return {
      post: {
        id: uid(),
        caption: "",
        location: "",
        photo: null,
        date: Date.now()
      }
    };
  },
  methods: {
    initCamera() {
      navigator.mediaDevices
        .getUserMedia({ video: true })
        .then(stream => (this.$refs.video.srcObject = stream));
    }
  },
  mounted() {
    this.initCamera();
  }
};
</script>

<style lang="sass">
.camera-frame
  border: 2px solid $grey-10
  border-radius: 10px
</style>
