<template>
  <ContentLoader v-if="!serialNumberExchange" />
  <div v-else class="tab_page exchange_record active">
    <span v-if="serialNumberExchange.length === 0" class="zero_text"
      >尚無兌換贈品</span
    >
    <div v-else class="table">
      <div class="th">
        <div class="row">
          <div class="grid">
            <span>兌換日期</span>
          </div>
          <div class="grid">
            <span>兌換項目</span>
          </div>
          <div class="grid">
            <span>狀態</span>
          </div>
        </div>
      </div>
      <div class="td">
        <div class="td_wrap">
          <div
            v-for="(itm, idx) in result"
            :key="itm.id"
            class="row"
            :style="{ animationDelay: `${idx * 0.1}s` }"
          >
            <div class="grid">
              <p>{{ formateDate(itm.exchange_date) }}</p>
            </div>
            <div class="grid">
              <p>{{ itm.exchange_item }}</p>
              <p>
                <span v-if="itm.lottery" class="lottery_text">(抽獎)</span><span :class="{lottery_color: itm.lottery}">{{ itm.exchange_point }}點</span
                >
              </p>
            </div>
            <div class="grid">
              <p
                v-for="(str, idx) in formateStr(itm.exchange_status_str)"
                :key="str + idx"
                :style="{ color: isDrawComplete(idx, itm.exchange_status)}"
              >
                {{ str }}
              </p>
            </div>
          </div>
        </div>
        <SerialNumberNavigation
          :prev="prev"
          :next="next"
          :currentPage="currentPage"
          :lastPage="lastPage"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SerialNumberNavigation from '@/components/SerialNumberNavigation';
import ContentLoader from '@/components/ContentLoader';
import { useArrayPagination } from 'vue-composable';

export default {
  components: { SerialNumberNavigation, ContentLoader },
  props: {
    serialNumberExchange: {
      type: Array,
    },
  },
  setup(props) {
    if (!props.serialNumberExchange) return;
    const exchangeList = props.serialNumberExchange.map((itm, idx) => {
      return { ...itm, id: idx };
    });
    const { result, next, prev, currentPage, lastPage } = useArrayPagination(
      exchangeList,
      { pageSize: 6 }
    );
    return { result, next, prev, currentPage, lastPage };
  },
  methods: {
    formateDate(date) {
      return date.replace('年', '/').replace('月', '/').replace('日', '');
    },
    formateStr(data) {
      return data.split('##');
    },
    isDrawComplete(idx, status){
      return idx === 1 && status === 4 ? '#ff2f37' : ''
    }
  },
};
</script>

<style lang="scss">
@import './SerialNumberExchange.scss';
</style>
