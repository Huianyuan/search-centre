<template>
  <div class="index-page">
    <a-input-search
      v-model:value="searchParams.text"
      placeholder="input search text"
      enter-button="Search"
      size="large"
      @search="onSearch"
    />
    <!--{{ JSON.stringify(postList) }}-->
    <!--<MyDivider />-->

  </div>
  <div>
      <a-tabs v-model:activeKey="activeKey" @change="onTabChange">
          <a-tab-pane key="post" tab="文章">
              <PostList :post-list="postList"/>
          </a-tab-pane>
          <a-tab-pane key="picture" tab="图片">
              <PictureList />
          </a-tab-pane>
          <a-tab-pane key="user" tab="用户">
              <UserList :user-list="userList"/>
          </a-tab-pane>
      </a-tabs>
  </div>
</template>

<script setup lang="ts">
import { ref, watchEffect } from "vue";
import PostList from "@/components/PostList.vue";
import PictureList from "@/components/PictureList.vue";
import UserList from "@/components/UserList.vue";
import { useRoute, useRouter } from "vue-router";
import myAxios from "@/plugins/myAxios";

const postList=ref([]);

myAxios.post("/post/list/page/vo",{}).then((res:any) => {
  postList.value=res.records;
});

const userList=ref([]);

myAxios.post("/user/list/page/vo",{}).then((res:any) => {
    userList.value=res.records;
});

const route = useRoute();
const router = useRouter();
const activeKey = route.params.category;
const initSearchParams = {
  text: "",
  pageSize: 10,
  pageNumber: 1,
};
const searchParams = ref(initSearchParams);

watchEffect(() => {
  searchParams.value = {
    ...initSearchParams,
    text: route.query.text,
  } as any;
});
const onSearch = (searchValue: string) => {
  alert(searchValue);
  router.push({
    query: searchParams.value,
  });
};

const onTabChange = (key: string) => {
  router.push({
    path: `/${key}`,
    query: searchParams.value,
  });
};
</script>
<style>
.index-page{
    text-align: center;
}
</style>