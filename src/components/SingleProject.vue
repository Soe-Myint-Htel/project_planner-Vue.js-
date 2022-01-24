<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="flexing">
      <div>
        <h3 @click="showDetail = !showDetail">{{ project.title }}</h3>
      </div>
      <div>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }" class="edit">
          <span class="material-icons"> edit </span>
        </router-link>
        <span class="material-icons" @click="completeProject"> done </span>
      </div>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api: "http://localhost:3000/project/",
    };
  },
  methods: {
    deleteProject() {
      let deleteRoute = this.api + this.project.id;
      fetch(deleteRoute, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    completeProject() {
      let competeRoute = this.api + this.project.id;
      fetch(competeRoute, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
        .then(() => {
          this.$emit("complete", this.project.id);
          auarrcrdrdedfEda;
          aakdkjkljfakljfljfffl;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
.project {
  padding: 15px;
  background-color: rgb(208, 224, 238);
  margin: 10px;
  border-left: 6px solid rgb(230, 35, 35);
  border-radius: 13px;
}
h3 {
  color: rgb(5, 105, 105);
  cursor: pointer;
}
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
span {
  margin-left: 13px;
  color:rgb(31, 23, 23);
}
span:hover {
  color: rgb(126, 118, 204);
  cursor: pointer;
}
.complete {
  border-left-color: rgb(143, 218, 31);
}
.edit {
  color:rgb(31, 23, 23);
}
</style>