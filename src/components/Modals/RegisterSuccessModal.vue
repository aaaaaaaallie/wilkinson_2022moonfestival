<template>
  <AppModal :header="true" :body="true" :footer="true" :close="closeModal">
    <template #header>
      <span>恭喜您!</span>
    </template>

    <template #body>
      <span>序號已上傳成功</span>
      <span><a style="color: #febd00">請保留小卡</a>以供審查</span>
    </template>

    <template #footer>
      <div class="btns">
        <AppButton :to="{ name: 'serial-number' }" ga="register-serialNumber">
          <span>我的序號</span>
        </AppButton>
        <AppButton :to="{ name: 'exchange' }" ga="register-exchange">
          <span>贈品兌換</span>
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
  methods: {
    closeModal() {
      this.$store.dispatch('showModal', '');
    },
  },
};
</script>
