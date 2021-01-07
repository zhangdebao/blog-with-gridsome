<template>
  <Layout>
    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="`/post/${edge.node.id}`">
              <h2 class="post-title">
                {{edge.node.title}}
              </h2>
              <!-- <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3> -->
            </g-link>
            <p class="post-meta">Posted by
              <a href="#">{{ edge.node.admin_user.firstname + edge.node.admin_user.lastname }}</a>
              on {{ edge.node.created_at }}</p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <a href="" >{{tag.title}} &nbsp;&nbsp;</a>
              </span>
          </div>
          <hr>
          <!-- Pager -->
          <!-- <div class="clearfix">
            <a class="btn btn-primary float-right">OLDER POSTS &rarr;</a>
          </div> -->
          <Pager :info="$page.posts.pageInfo"/>
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query ($page: Int){
  posts: allStrapiPost (perPage: 2, page: $page) @paginate {
    pageInfo {
      totalPages,
      currentPage
    }
    edges {
      node {
        id,
        title,
        admin_user {
          id,
          firstname,
          lastname
        }
        tags {
          id,
          title
        },
        created_at
      }
    }
  }
}
</page-query>
<script>
import { Pager } from 'gridsome'
export default {
  name: 'HomePage',
  components: {
    Pager,
  },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>

<style scoped>
</style>>
</style>
