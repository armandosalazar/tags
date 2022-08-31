<!-- Options API -->
<script>
export default {
  data() {
    return {
      currentValue: "",
      tags: [],
    };
  },
  methods: {
    handleKeyDown(evt) {
      const exists = this.tags.some((item) => item === this.currentValue);
      if (!exists)
        if (evt.key === "Enter" && this.currentValue !== "") {
          this.tags.push(this.currentValue);
          this.currentValue = "";
        }
    },
    handleSubmit() {
      if (this.currentValue !== "") {
        this.tags.push(this.currentValue);
      }
    },
    deleteTag(tag) {
      this.tags = this.tags.filter((item) => item !== tag);
    },
  },
};
</script>

<template>
  <h1>Tags</h1>
  <div class="inputTag">
    <input type="text" v-model="currentValue" @keydown="handleKeyDown" />
    <!-- Otra forma de hacerlo -->
    <!-- <form @submit.prevent="handleSubmit">
        <input type="text" v-model="currentValue">
      </form> -->
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }}
        <span class="material-symbols-sharp" @click="deleteTag(tag)">
          close
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
  h1 {
    margin-top: 40px;
  }
  .inputTag {
    width: 90%;
    margin: 0 auto;
  }

  .inputTag input {
    margin: 20px 0;
  }

  .tags {
    max-width: 100%;
    display: flex;
    /* overflow: auto; */
    flex-wrap: wrap;
  }

  .tag {
    padding: 2px 4px 2px 10px;
    display: flex;
    align-items: center;
    border: 1px solid #ccc;
    margin: 5px;
    border-radius: 3px;
  }

  .tag span {
    cursor: pointer;
    font-size: 20px;
  }
</style>
