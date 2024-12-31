

<template>
  <div>
    <div style="display: flex; grid-gap: 20px;" >
      <div style="flex: 1; padding: 20px;" class="card">
        <div style="display: flex; align-items: center; ">
          <div style="font-weight: bold; font-size: 18px; flex: 1;">{{data.film.name}}</div>
          <div>
            <el-button type="primary" plain>写短评</el-button>
            <el-button type="success" plain>写长评</el-button>
          </div>
        </div>

        <div style="margin-bottom: 20px">
          <el-rate v-model="data.film.score" disabled allow-half show-score></el-rate>
        </div>

        <div style="display: flex; grid-gap: 20px">
          <img :src="data.film.cover" alt="" style="width: 200px; height: 270px; border-radius: 5px;">
          <div style="flex: 1; color: #666">
            <div style="margin-bottom: 10px; "><strong>导演：</strong>{{data.film.director}}</div>
            <div style="margin-bottom: 10px; "><strong>主演：</strong>{{data.film.actors}}</div>
            <div style="margin-bottom: 10px; "><strong>类型：</strong>{{data.film.categoryName}}</div>
            <div style="margin-bottom: 10px; "><strong>制片国家/地区：</strong>{{data.film.country}}</div>
            <div style="margin-bottom: 10px; "><strong>语言：</strong>{{data.film.language}}</div>
            <div style="margin-bottom: 10px; "><strong>上映日期：</strong>{{data.film.date}}</div>
            <div style="margin-bottom: 10px; "><strong>片长：</strong>{{data.film.duration}}</div>
            <div style="margin-bottom: 10px; "><strong>IMDB：</strong>{{data.film.imdb}}</div>
          </div>
        </div>

        <div style="font-size: 20px; color: #1967e3">{{data.film.name}}的剧情简介</div>
        <div style="color: #666; text-indent: 2rem; line-height: 24px; text-align: justify">{{data.film.discription}}</div>

      </div>

      <div></div>
      <div style="width: 300px" class="card">
        <div style="font-size: 20px; font-weight: bold; margin-bottom: 20px">推荐电影</div>
        <div style="margin-bottom: 20px" v-for="item in data.recommendList" :key="item.id">
          <img src="item.cover" alt="" style="width: 100%">
          <div style="margin: 5px 0; font-size: 20px">{{item.name}}</div>
          <div>
            <el-rate v-model="item.score" disabled="disabled" allow-half show-score></el-rate>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>




<script setup>
import {reactive} from "vue";
import router from "@/router";
import request from "@/utils/request";

const data = reactive({
  id: router.currentRoute.value.query.id,
  film: {},
  recommendList: []
})

request.get('/film/selectById/' + data.id).then(res => {
  data.film = res.data
})

request.get('/film/selectRecommend').then(res => {
  data.recommendList = res.data
})
</script>



<style scoped>

</style>