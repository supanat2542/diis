<template>
  <q-layout view="lHh Lpr lFf">
    <!-- <q-header class="q-ma-sm bg-blue-grey-1">
      <q-toolbar class="bg-primary-gradient rounded-borders-10 shadow-5">
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title> Mable Admin Dashboard</q-toolbar-title>
      </q-toolbar>
    </q-header> -->

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      content-class="bg-blue-grey-1"
      class="bg-space-gradient"
    >
      <div class="q-ma-sm rounded-borders-20 bg-primary-gradient fixed-full shadow-15">
        <div class="text-center q-ma-xl">
          <q-avatar square size="80px">
            <img id="profile-image" src="~assets/logo.jpg" alt="no img" />
          </q-avatar>
          <div class="text-h5 text-white q-mt-sm">Mable</div>
          <div class="text-white text-grey-5">Smart BLE Scanner Network</div>
        </div>
        <q-list>
          <EssentialLink
            v-for="link in essentialLinks"
            :key="link.title"
            v-bind="link"
          />
        </q-list>
      </div>
    </q-drawer>

    <q-page-container class="bg-blue-grey-1">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from "components/EssentialLink.vue";

const linksData = [
  {
    title: "Home",
    caption: "แดชบอร์ดภาพรวมระบบ",
    icon: "fas fa-home",
    link: "#/index",
  },
  {
    title: "Map",
    caption: "แผนที่ติดตามตำแหน่งผู้ใช้งาน",
    icon: "fas fa-map",
    link: "#/map",
  },
  {
    title: "Reports",
    caption: "รายงานการใช้งาน",
    icon: "fas fa-chart-bar",
    link: "#/report",
  },
  {
    title: "Log out",
    caption: "ตั้งค่า",
    icon: "fas fa-sliders-h",
    link: "#/",
  },
];

export default {
  name: "MainLayout",
  components: { EssentialLink },
  data() {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData,
    };
  },
};

</script>

<style>
  #profile-image{
    border-radius: 50%;
  }
</style>
