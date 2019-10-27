<template>
  <section class="main">
    <div class="container">
      <div class="left-main-container">
        <div class="m-left">
          <project-list :projects="projectPage.results" />
          <pagination :page="projectPage.page" url-prefix="/projects/" />
        </div>
        <div class="m-right">
          
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import ProjectList from '~/components/ProjectList'
import Pagination from '~/components/Pagination'
export default {
  components: {
    ProjectList, Pagination
  },
  head() {
    return {
      title: this.$siteTitle('开源项目'),
      meta: [
        { hid: 'description', name: 'description', content: this.$siteDescription() },
        { hid: 'keywords', name: 'keywords', content: this.$siteKeywords() }
      ]
    }
  },
  async asyncData({ $axios, params }) {
    const [projectPage] = await Promise.all([
      $axios.get('/api/project/projects', {
        params: {
          page: params.page || 1
        }
      })
    ])
    return {
      projectPage: projectPage
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
