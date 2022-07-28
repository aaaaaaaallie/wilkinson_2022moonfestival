<template>
  <section class="comingSoon">
    <div class="wrap">
      <div class="content">
        <h2>coming soon...</h2>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  beforeCreate() {
    console.log('ok')
    if (this.$store.state.comingSoon) return;
    this.$router.replace({ name: 'home' });
  },
};
</script>

<style lang="scss" scoped>
@import './ComingSoon.scss';
</style>
