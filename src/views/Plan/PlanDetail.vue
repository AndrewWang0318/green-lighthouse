<template>
  <div class="page-plan-detail">
    <div class="row-banner">
      <van-count-down millisecond :time="time" format="HH:mm:ss:SS" />
    </div>

    <div class="row-plan-list">
      <van-swipe-cell v-for="v in plan_list">
        <!-- <template #left>
          <van-button square type="primary" text="选择" />
        </template> -->
        <van-cell class="item-row-plan-list" :border="false" :title="v.title" :value="v.is_done ? '已完成' : '未完成'" />
        <template #right>
          <van-button square type="danger" text="删除" />
          <van-button square type="primary" text="收藏" />
        </template>
      </van-swipe-cell>
    </div>
    <div class="btn-add-plan"></div>
    <div class="btn-change-theme"></div>
    <div class="btn-plan-list"></div>
  </div>
</template>

<script>
export default {
  name: 'PlanPage'
}
</script>


<script setup>
 import { ref, reactive } from 'vue'
  import { useRouter } from 'vue-router';
  import { useStore } from '@/stores/stores';
  import $tool from "@/utils/tool";
  import base_url from '@/request/base_url'
  import moment from 'moment';

  const now_time = moment();
  const end_time = moment().endOf('day') //当天23点59分59秒以13位Unix时间戳输出（毫秒）;
  const diff_milliseconds = end_time.diff(now_time,"milliseconds")

  const time = ref(diff_milliseconds);
  const plan_list = ref([
    {
      title:"睡前刷牙,洗脚,护肤",
      is_done:0,
    },
    {
      title:"看书一小时",
      is_done:0,
    },
    {
      title:"健身",
      is_done:0,
    },
    {
      title:"练吉他半小时",
      is_done:0,
    },
  ])

</script>

<style lang="scss" scoped>
@import "@/assets/sass/Plan/PlanDetail.scss";
</style>