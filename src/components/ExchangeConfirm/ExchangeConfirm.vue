<template>
  <div class="page confirm_page">
    <div class="change_box change_list1">
      <AppSubtitle>本次<br>兌換</AppSubtitle>
      <div class="table">
        <div class="wrap">
          <div class="t_header">
            <div class="row">
              <div class="grid">
                <span>兌換項目</span>
              </div>
              <div class="grid">
                <span>數量</span>
              </div>
              <div class="grid">
                <span>小計</span>
              </div>
            </div>
          </div>
          <div class="t_body">
            <div
              v-for="prize in selectedPrizes"
              :key="prize.awards_id"
              class="row"
            >
              <div class="grid">
                <p>
                  {{ prize.awards_item }} <span v-if="prize.lottery" class="lottery">(抽獎)</span><span class="lottery point-color" :class="{lottery_color: prize.lottery}">{{ prize.awards_points }} 點</span>
                  
                </p>
              </div>
              <div class="grid">
                <p>{{ prize.quantity }}</p>
              </div>
              <div class="grid">
                <p>{{ Number(prize.awards_points) * Number(prize.quantity) }}</p>
              </div>
            </div>
          </div>
          <div class="t_footer">
            <div class="row">
              <!-- <div class="grid">
                <span
                  >總計<span class="italic">{{ totalPoints }}</span
                  >點</span
                >
              </div> -->

              <div class="grid">
                <p>總計</p>
              </div>
              <div class="grid"></div>
              <div class="grid">
                <p>{{ totalPoints }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="change_box change_list2">
      <AppSubtitle>寄送<br>資料</AppSubtitle>
      <ExchangeConfirmUserForm
        :changePage="changePage"
        :prizes="selectedPrizes"
      />
    </div>
  </div>
</template>

<script>
import AppSubtitle from '@/components/AppSubtitle';
import ExchangeConfirmUserForm from '@/components/ExchangeConfirmUserForm';

export default {
  components: {
    AppSubtitle,
    ExchangeConfirmUserForm,
  },
  props: {
    changePage: {
      type: Function,
      required: true,
    },
    selectedPrizes: {
      type: Array,
      required: true,
    },
  },
  computed: {
    totalPoints() {
      return this.selectedPrizes.reduce(
        (total, { quantity, awards_points }) =>
          (total += Number(quantity) * Number(awards_points)),
        0
      );
    },
  },
};
</script>

<style lang="scss">
@import './ExchangeConfirm.scss';
</style>
