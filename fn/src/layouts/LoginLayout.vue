<template>
  <q-layout view="lHh Lpr lFf">
      <q-toolbar class="tab-bar">
        <q-toolbar-title style="font-size:50px;margin : 10px;">   
   <q-img class="title-photo" src="~assets/psulogo.png" native-context-menu></q-img>
        </q-toolbar-title>

       <a class="active"> BY ManaLab PSU</a>
      </q-toolbar>    
    <q-page-container>
      <router-view />
    </q-page-container>
  
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      tab: 'mails'
    }
  }
}
</script>

<style lang="scss" scoped>
$center: center;
$bold: bold;
$inset: inset;
$menu-bar-color: lightgray;
  .profile-image{
    border-radius: 50%;
    width:50%;
  }
  .text-center{
    text-align: $center;
    border-bottom-style: $inset;
    border-bottom-width: 1px;
    border-color: $menu-bar-color;
  }
  .text-head-center{
    text-align: $center;
    text-shadow: 2px;
  }
   .title-photo{
    width:40%;
    text-align: center;
    margin: auto;
  }
  a {
  color: #2b2a2a;
  display:inline-block;
  text-decoration: none;
  font-weight: 400;
}


</style>
