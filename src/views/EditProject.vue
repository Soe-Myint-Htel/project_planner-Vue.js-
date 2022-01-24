<template>
  <h2>Edit Project</h2>
  <form @submit.prevent="updateProject">
    <label>Project Title</label>
    <input type="text" v-model="title" />
    <label>Project Detail</label>
    <input type="text" v-model="detail" />
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  methods: {
    updateProject() {
      fetch("http://localhost:3000/project/" + this.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  mounted() {
    fetch("http://localhost:3000/project/" + this.id)
      .then((res) => {
        return res.json();
      })
      .then((datas) => {
        this.title = datas.title;
        this.detail = datas.detail;
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style>
</style>