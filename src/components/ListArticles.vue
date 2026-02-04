<template>
 
  <main class="list-articles">
    <div class="list-articles__container">
      <div class="list-articles__list">
        <CardArticle 
        v-for="item in newsList"
        :key="item.id"
        :id="item.id"
        :title="item.title"
        :description="item.body"
        class="list-articles__card" 
        />
      </div>
      <ThePaginator 
      :page="page"
      :totalPages="totalPages"
      @setPage="setPages"
      class="list-articles__paginator" />
    </div>
  </main>
</template>

<script>
  import CardArticle from "@/components/card/CardArticle.vue";
import ThePaginator from "@/components/ThePaginator.vue";

  export default {
    components: {
      CardArticle,
      ThePaginator
    },
    data() {
      return {
        newsList: [],
        limit: 10,
        page: 1,
        totalCount: 1,
        totalPages: 1
      };
    },
    methods: {
      getNewsList(page = 1) {
        this.$axios("https://dummyjson.com/posts", {
          params: {
            limit: this.limit,
            skip: this.limit * (page -1)
          }
        }).then((response) => {
          if (response?.data?.posts) {
            this.newsList = response.data.posts;
            this.page = page;
            this.totalCount = response.data.total;
            this.totalPages = Math.ceil(this.totalCount/this.limit);
          }
        });
      },
      setPages(page) {
        this.getNewsList(page)
      }
    },
    created () {
      this.getNewsList();
    }
  };
</script>

<style lang="less">
  .list-articles {
    padding-bottom: 20px;

    &__container {
      .container();
    }
    &__card {
      margin-bottom: 15px;
    }
  }
</style>