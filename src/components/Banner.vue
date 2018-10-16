<template>
    <div class="bitcoin-banner">
        <h1 class="bitcoin-banner__title">{{ mainTitle }}</h1>
        <h3 class="bitcoin-banner__blurb">{{ mainBlurb }}</h3>
    </div>
</template>
<script>
export default {
    props: ['mainTitle', 'mainBlurb']
}
</script>
<style lang="scss">
@import '../scss/variables';
.bitcoin-banner {
    text-align: center;
    width: calc(100% - 40px);
    padding: 10px;
    margin: 20px auto;
    background-color: $dark-transparent;
    &__title {
        font-size: 3rem;
    }
}
</style>