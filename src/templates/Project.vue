<template>
  <Layout>
    <div class="project info">
      <div class="container">
        <div class="project-header">
          <h1 class="project-title">{{ $page.project.title }}</h1>
          <div class="project-info">
            <div class="categories-container">
              <div class="categories">
                <span class="label">Categories</span>
                <span
                  class="category"
                  v-for="type in $page.project.types"
                  :key="type.id"
                  >{{ type.title }}</span>
              </div>
            </div>
            <div class="year-container">
              <span class="label">Year</span>
              <div>{{ $page.project.year }}</div>
            </div>
          </div>
        </div>
        <div class="content" v-html="messageHtml"></div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query($id: ID!) {
    project: strapiProject(id: $id) {
      title
      year
      message
      created_at
      types {
        id
        title
      }
    }
  }
</page-query>

<script>
export default {
  computed: {
    messageHtml() {
      let str = this.$page.project.message
      let match = str.match(/\!\[.*?\.jpg\)/g)
      match && match.forEach(item => {
        let path = item.match(/\(.*?\.jpg\)/g)[0]
        path = path.replace(/\(|\)/g, '')
        let img = `<img src="/uploads/${path}" style="width: 100%;"/>`
        str = str.replace(item, img)
      })
      return str
    }
  }
};
</script>

<style></style>
