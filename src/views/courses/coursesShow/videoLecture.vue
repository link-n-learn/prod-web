<!-- eslint-disable vue/valid-template-root -->
<template>
  <div class="container text-center">
    <h1>{{ Course.title }}</h1>
  </div>
  <div class="container">
    <iframe :src="embedUrl" width="90%" height="515"></iframe>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      videoUrl: "",
      embedUrl: "",
      Course: {},
    };
  },
  mounted() {
    setTimeout(() => {
      this.$store.dispatch("setMsgandError");
    }, 5000);
  },
  computed: mapGetters(["getfoundCourse"]),
  async beforeMount() {
    // var arrayLength = this.getfoundcourse.content.length;
    // console.log(arrayLength);

    console.log(this.getfoundCourse.content);
    for (var item in this.getfoundCourse.content) {
      // console.log(item);
      // console.log(this.getfoundCourse.content[item]);
      for (var j in this.getfoundCourse.content[item].secContent) {
        if (
          this.getfoundCourse.content[item].secContent[j]._id ==
          this.$route.params.lecture_id
        ) {
          this.Course = this.getfoundCourse.content[item].secContent[j];
          this.videoUrl = this.Course.link;
          this.videoUrl += "&";
          console.log(this.videoUrl);
          const videoId = this.videoUrl.substring(
            this.videoUrl.indexOf("=") + 1,
            this.videoUrl.indexOf("&")
          );
          this.embedUrl = `https://www.youtube.com/embed/${videoId}`;
          console.log(this.embedUrl);
          break;
        }
      }
    }
  },
};
</script>

<style scoped></style>
