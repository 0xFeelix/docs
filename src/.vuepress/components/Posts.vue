<template>
  <div class="post-container">
    <router-link v-for="(page, index) in pages" :to="page.path" :key="index">
      <div class="post-card">
        <div class="page-detail">
          <div class="page-title">{{ page.title }}</div>
          <!-- <div class="page-description">{{ page.frontmatter.description }}</div> -->
          <!-- <div class="page-author">Author: {{ page.frontmatter.author }}</div> -->
        </div>
      </div>
    </router-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pages: [],
    };
  },
  mounted() {
    this.$site.pages.forEach((page) => {
      if (page.frontmatter.type === "article") {
        this.pages.push(page);
      }
    });
  },
};
</script>

<style scoped>
.post-container {
  display: flex;
  flex-wrap: wrap;
}
.post-card {
  width: 200px;
  height: 100px;
  margin: 10px;
  border-top: 4px solid #31313a;
  background: #21212186;
  border-radius: 3px;
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}
.page-title {
  color: #ccc;
}
.page-title:hover {
  text-decoration: none !important;
}
.post-card:hover .page-title {
  color: #42b983;
}
.post-card:hover{
  background: #212121;
}
</style>