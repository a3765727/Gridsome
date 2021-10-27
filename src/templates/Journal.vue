<template>
  <Layout :sticky="false">
    <div class="journal info">
      <div class="container journal-container">
        <div class="journal-header">
          <h1 class="journal-title">{{ $page.journal.title }}</h1>
          <div class="journal-meta">
            <div class="journal-author">
              <span class="label">Author</span
              ><span class="author-name">{{ $page.journal.author }}</span>
            </div>
            <div class="journal-date">
              <span class="label">Date</span>
              <div>{{ $page.journal.date }}</div>
            </div>
            <div class="journal-time">
              <span class="label">Time</span><span>1 min read</span>
            </div>
          </div>
        </div>
        <div class="journal-content" v-html="messageHtml"></div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query($id: ID!) {
  journal: strapiJournal(id: $id) {
    id
    title
    abstract
    author
    message
    date: created_at (format: "D. MMM YYYY")
  }
}
</page-query>

<script>
export default {
  computed: {
    messageHtml() {
      let str = this.$page.journal.message
      let match = str.match(/\!\[.*?\.jpg\)/g)
      match && match.forEach(item => {
        let path = item.match(/\(.*?\.jpg\)/g)[0]
        path = path.replace(/\(|\)/g, '')
        let img = `<img src="${path}" style="width: 100%;"/>`
        str = str.replace(item, img)
      })
      return str
    }
  }
};
</script>

<style>
.journal-header {
  padding: 2rem 0 4rem
}
</style>
