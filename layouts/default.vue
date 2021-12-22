<template>
  <a-layout id="components-layout-demo-fixed-sider">
    <Sidebar />
    <a-layout :style="{ marginLeft: '200px' }">
      <Header />
      <a-layout-content :style="{ margin: '24px 16px 0', overflow: 'initial' }">
        <Nuxt />
      </a-layout-content>
      <Footer />
    </a-layout>
  </a-layout>
</template>

<script>
import Header from '~/components/layouts/Header.vue'
import Sidebar from '~/components/layouts/Sidebar.vue'
import Footer from '~/components/layouts/Footer.vue'
export default {
  name: 'DefaultLayout',
  components: {
    Header,
    Sidebar,
    Footer,
  },
}
</script>

<style>
#components-layout-demo-fixed-sider .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
</style>
