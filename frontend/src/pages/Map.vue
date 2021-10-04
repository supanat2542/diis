<template>
  <q-page class="q-pa-sm">
    <section-header
      title="Map"
      subTitle="แสดง Tag ติดตาม ณ เวลาปัจจุบัน"
    ></section-header>
    <div class="row">
      <div class="col q-ma-md">
        <div class="text-h4 text-primary" style="margin-left: 30px">
          Floor 1
        </div>
      </div>
    </div>
    <div class="container">
      <q-img class="profile-image" src="~assets/map_1.jpg" native-context-menu>
      </q-img>
      <!--------------------------- Location Hall --------------------------------- -->
      <div class="hall-1 row q-gutter-y-lg ">
        <template v-for="item in dashbord">
          <icon-map
            v-if="item.location == 'Hall'"
            :key="item.id"
            class="col-4"
            :id_visitor="item.visitor_id"
            :id="item.id"
            :fname="item.fname"
            :lname="item.lname"
            :tel="item.tel"
            :category="item.category"
            :room="item.location"
            :contract="item.contract"
            :timestamp="item.timestamp"
          ></icon-map>
        </template>
      </div>
      <!--------------------------- Location Room 103 --------------------------------- -->
      <div class="room-103 q-gutter-y-xl q-gutter-x-sm">
          <div v-for="item in dashbord" :key="item.id">
              <icon-map
              v-if="item.location == 103" 
                class="col"
                :id_visitor="item.visitor_id"
                :id="item.id"
                :fname="item.fname"
                :lname="item.lname"
                :tel="item.tel"
                :category="item.category"
                :room="item.location"
                :contract="item.contract"
                :timestamp="item.timestamp"
              ></icon-map>
          </div>
      </div>
      <!--------------------------- Location Room 105 --------------------------------- -->
      <div class="room-105 q-gutter-y-xl q-gutter-x-sm">
          <div v-for="item in dashbord" :key="item.id ">
              <icon-map
              v-if="item.location == 105" 
              class="col"
                :id_visitor="item.visitor_id"
                :id="item.id"
                :fname="item.fname"
                :lname="item.lname"
                :tel="item.tel"
                :category="item.category"
                :room="item.location"
                :contract="item.contract"
                :timestamp="item.timestamp"
              ></icon-map>
          </div>
      </div>
      <!--------------------------- Location Room 107 --------------------------------- -->
      <div class="room-107 row q-gutter-y-xl ">
        <template v-for="item in dashbord">
          <div v-if="item.location == 107" :key="item.id" class="col-4">
            <icon-map
              :id_visitor="item.visitor_id"
              :id="item.id"
              :fname="item.fname"
              :lname="item.lname"
              :tel="item.tel"
              :category="item.category"
              :room="item.location"
              :contract="item.contract"
              :timestamp="item.timestamp"
            ></icon-map>
          </div>
        </template>
      </div>
      <!--------------------------- Location Room 102 --------------------------------- -->
      <div class="room-102 row q-gutter-y-md">
        <template v-for="item in dashbord">
          <icon-map
            :key="item.id"
            class="col-4"
            v-if="item.location == 102"
            :id_visitor="item.visitor_id"
            :id="item.id"
            :fname="item.fname"
            :lname="item.lname"
            :tel="item.tel"
            :category="item.category"
            :room="item.location"
            :contract="item.contract"
            :timestamp="item.timestamp"
          ></icon-map>
        </template>
      </div>
    </div>
  </q-page>
</template>

<script>
import IconMap from "src/components/IconMap.vue";
import SectionHeader from "../components/SectionHeader.vue";
const moment = require("moment");
import { axios } from "boot/axios";
export default {
  components: {
    SectionHeader,
    IconMap,
  },
  data() {
    return {
      dashbord: [],
    };
  },
  async mounted() {
    setTimeout(function () {
      location.reload(1);
    }, 60000);
    //<------------------------- Connect Database ----------------------------------->
    const url = "http://localhost:3030/api/" 
    let resp = await axios.get(url+"visitors");
    this.list = resp.data.result.rows;
    console.warn("list item visitors");
    console.warn(this.list);
    let resp2 = await axios.get(url+"scanlog");
    this.list2 = resp2.data.result.rows;
    console.warn("list2 scanerlog");
    console.warn(this.list2);
    //<-------------------------Create Dashbord ----------------------------------->
    for (var i = 0; i < this.list.length; i++) {
      if (this.list[i].time_stop == null) {
        for (var j = 0; j < this.list2.length; j++) {
          if (this.list[i].tag_address == this.list2[j].device_address) {
            const newItem = {
              id: this.list[i].tag_id,
              fname: this.list[i].first_name,
              lname: this.list[i].last_name,
              tel: this.list[i].tel,
              contract: this.list[i].contract,
              category: this.list[i].category,
              location: this.list2[j].room,
              visitor_id: this.list[i].visitor_id,
              timestamp:moment(this.list2[j].scan_timestamp).format(),
            };
            this.dashbord.push(newItem);
            break;
          }
        }
      }
    }
    console.warn(this.dashbord);
  },
};
</script>

<style>
img {
  width: 65%;
  display: block;
  margin: 0 auto;
}
.hall-1 {
  position: absolute;
  top: 30%;
  left: 34.6%;
  width: 250px;
  height: 250px;
  overflow: hidden;
}
.room-102 {
  position: absolute;
  top: 52.5%;
  left: 48%;
  width: 250px;
  height: 220px;
  overflow: hidden;
}
.room-103 {
  position: absolute;
  top: 15%;
  left: 59%;
  width: 60px;
  height: 250px;
  overflow: hidden;
}
.room-105 {
  position: absolute;
  top: 19.5%;
  left: 63.8%;
  width: 70px;
  height: 250px;
  overflow: hidden;
}
.room-107 {
  position: absolute;
  top: 19.5%;
  left: 68.3%;
  width: 150px;
}
.container {
  position: relative;
}
</style>