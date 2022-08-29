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
  <div class="inputTag">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }}
        <span class="material-symbols-sharp" @click="deleteTag(tag)">
          close
        </span>
      </div>
    </div>
    <input type="text" v-model="currentValue" @keydown="handleKeyDown" />
    <!-- Otra forma de hacerlo -->
    <!-- <form @submit.prevent="handleSubmit">
        <input type="text" v-model="currentValue">
      </form> -->
  </div>
</template>

<style>
.tags {
  display: flex;
}
.tag {
  padding: 2px;
  display: flex;
  align-items: center;
  /* border: 1px solid #ccc; */
}
.tag span {
  cursor: pointer;
  /* font-size: 25px; */
}
</style>
