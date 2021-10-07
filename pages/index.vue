<template>
  <div class="home">
    <div class="title">
    <h1 v-if="$fetchState.pending">Hello Default</h1>
    <h1 v-else>{{ message }}</h1>
    </div>
    <div class="card-grid">
      <SmallCard
        v-bind:key="project.id"
        v-bind:title="project.name"
        v-bind:slug="project.slug"
        v-bind:id="project.id"
        v-for="project in projects"
      />
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import { ReactIcon } from "~/components/Icons.vue";
import SmallCard from "~/components/SmallCard.vue";
import { projects } from "../utils/projectsData";
export default {
  data() {
    return {
      projects: projects,
      message: 'Before loading'
    };
  },
  async fetch() {
    console.log('running the fetch function');
    const response = await fetch('/api/message?name=Sebastian');
    console.log('Response is ' + response);
    this.message = await response.json();
    console.log('after setting message');
  },
  fetchOnServer: false,
  created() {
    // console.log(projects);
  },
  components: {
    Logo,
    ReactIcon,
    SmallCard
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
