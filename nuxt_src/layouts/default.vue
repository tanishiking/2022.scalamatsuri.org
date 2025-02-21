<template>
  <div v-lazy-container="{ selector: 'img.lazy' }">
    <the-header />
    <nuxt />
    <lazy-component @show="hasShown">
      <sns v-if="snsFooterHasShown" />
    </lazy-component>
    <flow-sns v-if="$mq === 'lg'" />
    <the-footer />
  </div>
</template>

<i18n>
## language=yaml
  en:
    defaultSiteName: ScalaMatsuri 2022
    defaultSiteSubTitle: The largest international Scala conference in Asia
    defaultDescription: The largest international Scala conference in Asia.
    defaultUrl: https://scalamatsuri.org/
    opengraphUri: https://scalamatsuri.org/img/favicons/ogp_en.jpg
    twitterAccountId: '@scala_jp'
  ja:
    defaultSiteName: ScalaMatsuri 2022
    defaultSiteSubTitle: アジア最大級の Scala のカンファレンス
    defaultDescription: Scala をテーマにアジア最大級のカンファレンスが開催されます。
    defaultUrl: https://scalamatsuri.org/
    opengraphUri: https://scalamatsuri.org/img/favicons/ogp_ja.jpg
    twitterAccountId: '@scala_jp'
</i18n>

<script>
import theHeader from '@/components/parts/TheHeader.vue'
import sns from '@/components/parts/snsFooter.vue'
import flowSns from '@/components/parts/flowSns.vue'
import theFooter from '@/components/parts/TheFooter.vue'

export default {
  head() {
    // Script 内部で i18n を利用するサンプル
    const $t = this.$t.bind(this)
    return {
      title: $t('defaultSiteName'),
      titleTemplate: `%s | ${$t('defaultSiteSubTitle')}`,
      meta: [
        { charset: 'UTF-8' },
        { 'http-equiv': 'x-ua-compatible', content: 'ie=edge' },
        { name: 'viewport', content: 'width=device-width, initial-scale=1' },
        { name: 'description', content: `${$t('defaultSiteName')} | ${$t('defaultSiteSubTitle')}` },
        { name: 'keywords', content: 'Scala,スカラ,カンファレンス,ScalaMatsuri,2022' },
        { property: 'og:type', content: 'website' },
        { property: 'og:locale', content: 'ja_JP' },
        { property: 'og:url', content: $t('defaultUrl') },
        { property: 'og:title', content: `${$t('defaultSiteName')} | ${$t('defaultSiteSubTitle')}` },
        { property: 'og:site_name', content: $t('defaultSiteName') },
        { property: 'og:description', content: `${$t('defaultDescription')}` },
        { property: 'og:image', content: $t('opengraphUri') },
        { property: 'og:image:width', content: '1200' },
        { property: 'og:image:height', content: '630' },
        { name: 'twitter:card', content: 'summary_large_image' },
        { name: 'twitter:site', content: $t('twitterAccountId') },
        { name: 'twitter:creator', content: $t('twitterAccountId') },
        { name: 'twitter:url', content: 'https://twitter.com/scala_jp' },
        { name: 'twitter:title', content: `${$t('defaultSiteName')} | ${$t('defaultSiteSubTitle')}` },
        { name: 'twitter:description', content: $t('defaultDescription') },
        { name: 'twitter:image', content: $t('opengraphUri') },
        { name: 'og:image:secure_url', content: $t('opengraphUri'), hid: 'og:image:secure_url' },
        { name: 'application-name', content: 'ScalaMatsuri 2022' },
        { name: 'apple-mobile-web-app-title', content: 'ScalaMatsuri 2022' },
        { name: 'theme-color', content: '#2d88ef' },
        { name: 'msapplication-TileColor', content: '#2d88ef' },
        { name: 'msapplication-TileImage', content: '/img/favicons/mstile-144x144.png' },
        { name: 'google-site-verification', content: 'HliqkO_EksFAabDeL9H8LT1_F3sqTf3x7-aL9JIHaK4' }
      ],
      link: [
        { rel: 'icon', type: 'image/x-icon', href: '/img/favicons/favicon.ico' },
        { rel: 'shortcut icon', type: 'image/vnd.microsoft.icon', href: '/img/favicons/favicon.ico' },
        { rel: 'icon', type: 'image/vnd.microsoft.icon', href: '/img/favicons/favicon.ico' },
        { rel: 'icon', type: 'image/png', href: '/img/favicons/android-chrome-192x192.png', sizes: '192x192' },
        { rel: 'icon', type: 'image/png', href: '/img/favicons/favicon-16x16.png', sizes: '16x16' },
        { rel: 'icon', type: 'image/png', href: '/img/favicons/favicon-32x32.png', sizes: '32x32' },
        { rel: 'icon', type: 'image/png', href: '/img/favicons/favicon-48x48.png', sizes: '48x48' },
        { rel: 'icon', type: 'image/png', href: '/img/favicons/favicon-96x96.png', sizes: '96x96' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-57x57.png', sizes: '57x57' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-60x60.png', sizes: '60x60' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-72x72.png', sizes: '72x72' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-76x76.png', sizes: '76x76' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-114x114.png', sizes: '114x114' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-120x120.png', sizes: '120x120' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-144x144.png', sizes: '144x144' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-152x152.png', sizes: '152x152' },
        { rel: 'apple-touch-icon', href: '/img/favicons/apple-touch-icon-180x180.png', sizes: '180x180' },
        { rel: 'manifest', href: '/img/favicons/manifest.json' }
      ]
    }
  },
  components: {
    theHeader,
    flowSns,
    sns,
    theFooter
  },
  data() {
    return { snsFooterHasShown: false }
  },
  methods: {
    hasShown: function () {
      this.snsFooterHasShown = true
    }
  }
}
</script>

<style lang="scss">
img[lazy='loaded'] {
  opacity: 0;
  animation-name: fadein;
  animation-duration: .3s;
  animation-iteration-count: 1;
  animation-fill-mode: forwards;
  animation-direction: normal;
  animation-timing-function: ease-out;
  @keyframes fadein {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
}
</style>
