<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h3>{{ post.title }}</h3>
    <p class="pre">{{ post.body }}</p>
  </div>
  <div v-else>
    <Spinner />
  </div>
</template>

<script>
import getPost from "@/composables/getPost";
import Spinner from "../components/Spinner.vue";
import { useRoute } from "vue-router";

export default {
  props: ["id"],
  components: { Spinner },
  setup(props) {
    const route = useRoute();

    const { error, post, load } = getPost(route.params.id);

    load();

    return { error, post };
  },
};
</script>

<style scoped>
.post {
  margin: 0 40px 30px;
  padding-bottom: 30px;
  border-bottom: 1px dashed #e7e7e7;
}
.post h3 {
  display: inline-block;
  position: relative;
  font-size: 26px;
  color: white;
  margin-bottom: 10px;
  max-width: 400px;
}
.post h3::before {
  content: "";
  display: block;
  width: 100%;
  height: 100%;
  background: #609966;
  position: absolute;
  z-index: -1;
  padding-right: 40px;
  left: -30px;
  transform: rotateZ(-1deg);
}
.post p {
  color: #444;
  line-height: 1.5em;
  margin-top: 40px;
}
</style>
