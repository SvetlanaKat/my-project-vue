<template>
<div>
  <PageHeader />

 <RouterView />
</div>
</template>

<script>
import PageHeader from "@/components/PageHeader.vue";

  export default {
    components: {
      PageHeader,
    },
  };
</script>


<style lange="less">

</style>
