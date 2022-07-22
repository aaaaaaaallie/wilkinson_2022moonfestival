<template>
  <AppModal :header="true" :body="true" :footer="true">
    <template #header>
      <span>您的兌換申請已送出</span>
    </template>

    <template #body>
      <div class="exchange_success">
        <span>請耐心等候1-2個工作天</span>
        <span>待兌換審查無誤後，系統將會寄出通知信函</span>
        <span>再依步驟完成兌獎程序即可</span>
        <span class="light">※抽獎名單將於<a class="date">2022/9/26</a>公布</span>
      </div>
    </template>

    <template #footer>
      <div class="btns">
        <AppButton
          :to="`${baseURL}serial-number#exchange`"
          ga="exchange-finish"
        >
          <span>完成</span>
        </AppButton>
      </div>
    </template>
  </AppModal>
</template>

<script>
import AppModal from '@/components/AppModal';
import AppButton from '@/components/AppButton';

export default {
  components: {
    AppModal,
    AppButton,
  },
  props: ['resetPrizes', 'changePage'],
  computed: {
    baseURL() {
      return process.env.NODE_ENV === 'production'
        ? '/wilkinson_2022moonfestival/'
        : '/';
    },
  },
  methods: {
    closeModal() {
      // this.changePage('prizes');
      // this.resetPrizes();
      // this.$store.dispatch('showModal', '');
      this.$router.push(`${this.baseURL}serial-number#exchange`);
    },
  },
};
</script>

<style lang="scss">
@import '@/assets/scss/vars/index.scss';

.light {
  color: map-get($color, 'light');
}
</style>
