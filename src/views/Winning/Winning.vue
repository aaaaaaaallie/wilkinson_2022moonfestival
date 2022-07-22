<template>
  <InnerPageLayout>
    <section class="winner">
      <div class="wrap">
        <PageTitle>抽獎得獎名單</PageTitle>
         <div class="congrats mb">
            <span>恭喜得獎</span>
          </div>
        <div class="content">
          <div class="congrats pc">
            <span>恭喜得獎</span>
          </div>
          <div v-if="!isDrown">
            <WinningNotYet title="" />
          </div>
          <WinningList v-else />
          <div class="btns">
            <AppButton :to="{ name: 'home' }" ga="winning-back-to-home">
              <span>返回首頁</span>
            </AppButton>
          </div>
        </div>
      </div>
    </section>
  </InnerPageLayout>
</template>

<script>
import InnerPageLayout from '@/layouts/InnerPageLayout';
import PageTitle from '@/components/PageTitle';
import AppButton from '@/components/AppButton';
import WinningNotYet from '@/components/WinningNotYet';
import WinningList from '@/components/WinningList';

export default {
  components: {
    InnerPageLayout,
    PageTitle,
    AppButton,
    WinningNotYet,
    WinningList,
  },
  computed: {
    isDrown() {
      return this.$store.state.winnerList;
    },
  },
};
</script>

<style lang="scss">
@import './Winning.scss';
</style>
