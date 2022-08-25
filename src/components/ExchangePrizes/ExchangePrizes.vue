<template>
  <div class="page exchange_page">
    <div class="user_remaining_point">
      <UserName :name="$store.getters['auth/username']" />
      <div class="remaining_points">
        剩餘點數<span>{{ $store.getters['user/lastPoints'] }}</span
        >點
      </div>
    </div>
    <div id="exchange_form">
      <div class="prize" id="exchange_prize">
        <div class="table_title lottery">抽獎</div>
        <ContentLoader v-if="!isPrizesInit" />
        <div v-else class="input_group">
          <ExchangePrizesInput
            v-for="itm in lotteryPrizes"
            :key="itm.awards_id"
            :prize="itm"
          >
            <input
              class="exchange_item"
              type="number"
              placeholder="請輸入數量"
              min="0"
              inputmode="numeric"
              v-model.number="itm.quantity"
            />
          </ExchangePrizesInput>
        </div>
      </div>
      <div class="prize" id="lottery_prize">
        <div class="table_title exchange">點數<br>兌換</div>
        <ContentLoader v-if="!isPrizesInit" />
        <div v-else class="input_group">
          <ExchangePrizesInput
            v-for="itm in exchangePrizes"
            :key="itm.awards_id"
            :prize="itm"
          >
            <!-- <input
              v-if="typeof itm.awards_last_nu === 'string'"
              class="exchange_item"
              type="number"
              placeholder="請輸入數量"
              min="0"
              inputmode="numeric"
              v-model.number="itm.quantity"
            />
            <select
              v-else
              class="exchange_item"
              v-model.number="itm.quantity"
              :disabled="itm.awards_last_nu === 0"
            >
              <option value="" disabled>請輸入數量</option>
              <option
                v-for="(number) in itm.awards_last_nu"
                :key="itm.awards_item + number"
                :value="number"
              >
                {{ number }}
              </option>
            </select> -->
            <select
              class="exchange_item"
              v-model.number="itm.quantity"
              :disabled="itm.awards_last_nu === 0"
            >
              <option value="">請輸入數量</option>
              <option
                v-for="number in (itm.awards_last_nu === '∞' || itm.awards_last_nu >= 30 ? 30 : itm.awards_last_nu)"
                :key="itm.awards_item + number"
                :value="number"
              >
                {{ number }}
              </option>
            </select>

          </ExchangePrizesInput>
        </div>
      </div>
      <!-- <ExchangePrizesNotice /> -->
      <div class="btns">
        <AppButton
          id="check_btn"
          to="false"
          ga="exchange-prize-submit"
          @click="submit"
        >
          <span>送出</span>
        </AppButton>
      </div>
    </div>
  </div>
</template>

<script>
import UserName from '@/components/UserName';
// import AppSubtitle from '@/components/AppSubtitle';
import AppButton from '@/components/AppButton';
import ExchangePrizesInput from '@/components/ExchangePrizesInput';
// import ExchangePrizesNotice from '@/components/ExchangePrizesNotice';
import ContentLoader from '@/components/ContentLoader';

export default {
  components: {
    UserName,
    // AppSubtitle,
    AppButton,
    ExchangePrizesInput,
    // ExchangePrizesNotice,
    ContentLoader,
  },
  props: {
    changePage: {
      type: Function,
      required: true,
    },
    prizes: {
      type: Array,
      required: true,
    },
    selectedPrizes: {
      type: Array,
      required: true,
    },
  },

  computed: {
    hasSelectedPrizes() {
      return this.selectedPrizes.length !== 0;
    },

    totalPoint() {
      return this.selectedPrizes.reduce(
        (total, { quantity, awards_points }) => {
          return (total += Number(quantity) * Number(awards_points));
        },
        0
      );
    },

    isNotEnoughPoints() {
      return this.totalPoint > this.$store.getters['user/lastPoints'];
    },

    isPrizesInit() {
      return this.prizes.length !== 0;
    },

    lotteryPrizes() {
      return this.prizes.filter((itm) => itm.lottery);
    },

    exchangePrizes() {
      return this.prizes.filter((itm) => !itm.lottery);
    },

    // isSelectPrizes(itm){
    //   return itm.awards_last_nu === 'string' ? 30 : 30
    // }
  },
  mounted (){
    console.log(this.lotteryPrizes)
  },
  methods: {
    submit() {
      // alert('威金森 月來越強活動\n活動已結束，\n非常感謝各位熱烈的參與！')
      if (!this.hasSelectedPrizes) return alert('請選擇兌換項目');
      if (this.isNotEnoughPoints) return this.showNotEnoughPointPopup();
      this.showConfirmPage();
    },

    showNotEnoughPointPopup() {
      this.$store.dispatch('showModal', 'exchange/point');
    },

    showConfirmPage() {
      this.changePage('confirm');
      window.scrollTo(0, 0);
    },
  },
};
</script>

<style lang="scss" scoped>
@import './ExchangePrizes.scss';
</style>
