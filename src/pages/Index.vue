<template>
  <Layout>
    <div class="container">
      <div class="hero">
        <h1 class="hero-title">Simplicity. Aesthetics. Value.</h1>
        <h2 class="hero-subtitle">
          Hi there, I'm an independent Digital Designer &amp; Art Director
          focused on digital design for brands that like to have fun.
        </h2>
      </div>
      <div class="projects">
        <div
          class="project"
          v-for="project in $page.projects.edges"
          :key="project.node.id"
        >
          <a
            :href="`/project/${project.node.id}`"
            class="project-link"
          >
            <img
              alt="Banana"
              :src="`${GRIDSOME_API_URL}${project.node.cover.url}`"
              width="2560"
              class="thumbnail g-image g-image--lazy g-image--loaded"
            />
            <h3 class="project-title">{{ project.node.title }}</h3>
            <div class="categories">
              <span
                class="category"
                v-for="type in project.node.types"
                :key="type.id"
                >{{ type.title }}</span
              >
            </div>
          </a>
        </div>
      </div>
    </div>
    <div>
      <div class="latest-journals-heading container">
        <span class="label">Latest and greatest</span>
      </div>
      <div class="latest-journals">
        <div class="container">
          <a
            v-for="journal in $page.journals.edges"
            :key="journal.node.id"
            :href="`/journal/${journal.node.id}`"
            class="journal"
          >
            <h3 class="journal-title">{{ journal.node.title }}</h3>
          </a>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query {
    projects: allStrapiProject(order: ASC) {
      edges {
        node {
          id
          title
          cover {
            url
          }
          types {
            id
            title
          }
        }
      }
    }
    journals: allStrapiJournal(order: ASC) {
      edges {
        node {
          id
          title
        }
      }
    }
  }
</page-query>

<script>
import { Pager } from "gridsome";

export default {
  metaInfo: {
    title: "Home",
  },
  name: "Home",
  components: {
    Pager,
  },
};
</script>

<style>
.pager {
  text-align: center;
}
.pager > a {
  margin-right: 10px;
}
.pager > a:last-child {
  margin: 0;
}
</style>
