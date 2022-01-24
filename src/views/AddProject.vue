<template>
  <h2>Add Project</h2>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title" id="PTitle" />
    <label>Project Detail</label>
    <input type="text" v-model="detail" id="PDetail" />
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  methods: {
    addProject() {
      let titleValue = document.querySelector("#PTitle").value;
      let detailValue = document.querySelector("#PDetail").value;
      if (titleValue && detailValue) {
        fetch("http://localhost:3000/project", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            title: this.title,
            detail: this.detail,
            complete: false,
          }),
        })
          .then(() => {
            this.$router.push("/");
          })

          .catch(() => {});
      } else {
        if (!titleValue || !detailValue) {
          alert("Please fill out all fields!");
        }
      }
    },
  },
};
</script>

<style>
form {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
/* textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
} */
form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce98;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>