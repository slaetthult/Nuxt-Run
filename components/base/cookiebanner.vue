<template>

    <div v-if="showCookieBanner" class="cookiebanner">
      <div class="cookiebanner-layer">
        <div class="gridWrap">
          <div class="cookiebanner-layer-text w12 mw6 lw6">
            <p>
              This website is using cookies.
            </p>
          </div>
          <div class="cookiebanner-layer-actions w12 mw6 lw6">
            <button @click="acceptAll()" class="cookiebanner-actions-accept-all">Accept all cookies</button>
            <button @click="acceptFunctionals()" class="cookiebanner-actions-accept-functionals">Accept technical cookies</button>
          </div>
        </div>
      </div>
    </div>

</template>

<script>
import {getCookieValueOf, setCookie, deleteCookie} from '~/utils/cookies';

export default {
    props: [],
    data(){
        return {

          showCookieBanner: false

        }
    },
    mounted(){

      this.showInitially();

    },
    methods: {

      showInitially(){

        const _this = this;
        this.showCookieBanner = !getCookieValueOf('cookiesAcceptedAll') && !getCookieValueOf('cookiesAcceptedFunctionals');

        this.$nextTick(() => {

          if(_this.showCookieBanner){

            _this.ensureVisibleFooter();

          }

        });

      },

      acceptAll(){

        setCookie('cookiesAcceptedAll', 'true');
        this.showCookieBanner = false;

      },

      acceptFunctionals(){

        setCookie('cookiesAcceptedFunctionals', 'true');
        this.showCookieBanner = false;

      },

      ensureVisibleFooter(){

        const cookieBannerLayerHeight = this.$el.querySelectorAll(".cookiebanner-layer")[0].offsetHeight;

        this.$el.style.height = cookieBannerLayerHeight + 'px';

      }

    }
}
</script>

<style lang="scss" scoped>

  .cookiebanner-layer {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 20px 0;
    background: $color-white;
    z-index: $zLevel10;
    border-top: 1px solid $color-lightgrey;
  }

</style>
