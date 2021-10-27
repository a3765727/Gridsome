<template>
  <Layout>
    <div class="container">
      <div class="journal-hero">
        <h1 class="journal-header">
          a wise person once said...
        </h1>
      </div>
    </div>
    <a
      v-for="journal in $page.journals.edges"
      :key="journal.node.id"
      :href="`/journal/${journal.node.id}`"
      class="journal-post"
    >
      <div class="container journal">
        <h2 class="journal-title">{{ journal.node.title }}</h2>
        <p class="journal-excerpt">{{ journal.node.abstract }}</p>
      </div>
    </a>
  </Layout>
</template>

<page-query>
  query {
    journals: allStrapiJournal(order: ASC) {
      edges {
        node {
          id
          title
          abstract
        }
      }
    }
  }
</page-query>

<script>
export default {
  metaInfo: {
    title: "Journal",
  },
  name: "Journal",
};
</script>

<style>
.journal-header {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0
}
</style>