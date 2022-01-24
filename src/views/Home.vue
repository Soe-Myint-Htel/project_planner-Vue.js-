<template>
  <h1>Projects</h1>
  <FilterNav @filterValue="current = $event" :current="current"></FilterNav>
  <div v-for="project in filteredProjects" :key="project.id">
    <SingleProject
      :project="project"
      @delete="deleteProject"
      @complete="completeProject"
    ></SingleProject>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav";

import SingleProject from "../components/SingleProject";
export default {
  name: "Home",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    completeProject(id) {
      let findProject = this.projects.find((project) => {
        return project.id === id;
      });
      findProject.complete = !findProject.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === "complete") {
        return this.projects.filter((project) => {
          return project.complete;
        });
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => {
          return !project.complete;
        });
      }
      return this.projects;
    },
  },
  mounted() {
    fetch("http://localhost:3000/project")
      .then((response) => {
        return response.json();
      })
      .then((datas) => {
        this.projects = datas;
      })
      .catch(() => {});
  },
};
</script>
<style>
h1 {
  text-align: center;
}
</style>
