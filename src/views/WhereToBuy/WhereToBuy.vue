<template>
  <InnerPageLayout>
    <section class="channels">
      <div class="wrap">
        <PageTitle>購買通路</PageTitle>
        <div class="content">
          <AppSubtitle>網購通路</AppSubtitle>
          <div class="text">
            <div class="btns cannels_btns">
              <AppButton
                to="https://24h.pchome.com.tw/store/DBAG7D"
                ga="whereToBuy-PChome-origin"
                :icon="false"
              >
                <span>PChome</span>
              </AppButton>
              <AppButton
                to="https://www.momoshop.com.tw/category/DgrpC
ategory.jsp?d_code=2006200365&p_orderType=
6&showType=chessboardType"
                ga="whereToBuy-momo-origin"
                :icon="false"
              >
                <span>MOMO購物網</span>
              </AppButton>
            </div>
          </div>
          <AppSubtitle>實體通路</AppSubtitle>
          <!-- <div class="text">
            <div class="access_title">
              <span>品項</span>
              <span>通路</span>
            </div>
          </div> -->
          <div class="text">
            <div class="access_title">
              <span>品項</span>
              <span>通路</span>
            </div>
            <WhereToBuyAccess title="威金森保特瓶">
              <div class="store">
                <span
                  >全家、日藥本鋪、唐吉軻德</span
                >
              </div></WhereToBuyAccess
            >
            <WhereToBuyAccess title="威金森易開罐">
              <div class="store">
                <span
                  >家樂福、復興微風超市<br>
                  太平洋崇光百貨超市、唐吉軻德</span
                >
              </div>
            </WhereToBuyAccess>
            <WhereToBuyAccess title="威金森玻璃瓶">
              <div class="store">
                <span
                  >復興微風超市、唐吉軻德</span
                >
              </div>
            </WhereToBuyAccess>
          </div>
          <div class="btns">
            <AppButton :to="{ name: 'home' }" ga="whereToBuy-back-to-home">
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
import AppSubtitle from '@/components/AppSubtitle';
import AppButton from '@/components/AppButton';
import WhereToBuyAccess from '@/components/WhereToBuyAccess';

export default {
  components: {
    InnerPageLayout,
    PageTitle,
    AppSubtitle,
    AppButton,
    WhereToBuyAccess,
  },
};
</script>

<style lang="scss">
@import './WhereToBuy.scss';
</style>
