<template>
  <q-page class="q-pa-sm">
    <section-header
      title="Dashboard"
      subTitle="ศูนย์กลางการควบคุม"
    ></section-header>
    <!-------------------------- Driver Card ------------------------------------>
    <div class="row q-gutter-col-md">
      <div v-for="item in dashbord" :key="item.id" class="col-2">
        <div v-if="item.visitor_id != 0">
          <device-card
            :id="item.id"
            :fname="item.fname"
            :lname="item.lname"
            :tel="item.tel"
            :contract="item.contract"
            :category="item.category"
            :location="item.location"
            :visitor_id="item.visitor_id"
            :tag_address="item.tag_address"
            :time_start="item.time_start"
            :id_civiliz="item.id_civiliz"
          ></device-card>
        </div>
        <div v-else>
          <add-card :id="item.id"></add-card>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import SectionHeader from "../components/SectionHeader.vue";
import DeviceCard from "../components/DeviceCard.vue";
import AddCard from "../components/AddCard.vue";
import { axios } from "boot/axios";
const moment = require("moment");

export default {
  name: "PageIndex",
  components: {
    SectionHeader,
    DeviceCard,
    AddCard,
  },
  data() {
    return {
      dashbord: [],
    };
  },

  async mounted() {
    // setTimeout(function () {
    //   location.reload(1);
    // }, 60000);
    //<------------------------- Connect Database ----------------------------------->
    const url = "http://localhost:3030/api/";
    let resp = await axios.get(url + "visitors",300);
    this.list = resp.data.result.rows;
    console.warn("list item visitors");
    console.warn(this.list);

    let resp4 = await axios.get(url + "scanlog");
    this.list4 = resp4.data.result.rows;
    console.warn("list4 scanerlog");
    console.warn(this.list4);

    let resp5 = await axios.get(url + "tags");
    this.list5 = resp5.data.result.rows;
    console.warn("list5 tags");
    console.warn(this.list5);

    for (var i = 0; i < this.list5.length; i++) {
      // console.warn(this.list5[i].tag_address);
      for (var j = 0; j < this.list.length; j++) {
        if (
          this.list5[i].tag_address == this.list[j].tag_address &&
          this.list[j].time_stop == null
        ) {
          for (var k = 0; k < this.list4.length; k++) {
            if (this.list5[i].tag_address == this.list4[k].device_address) {
              const newItem = {
                id: this.list5[i].tag_id,
                visitor_id: this.list[j].visitor_id,
                fname: this.list[j].first_name,
                lname: this.list[j].last_name,
                tel: this.list[j].tel,
                contract: this.list[j].contract,
                category: this.list[j].category,
                location: this.list4[k].room,
                tag_address: this.list5[i].tag_address,
                time_start: moment(this.list[j].time_start).format(" hh:mm A"),
                id_civiliz: this.list[j].id_civiliz,
              };
              this.dashbord.push(newItem);
              console.warn("data : " + this.list5[i].tag_address);
              break;
            }
          }
          break;
        } else if (j == this.list.length - 1) {
          const newItem = {
            visitor_id: 0,
            tag_address: this.list5[i].tag_address,
            id: this.list5[i].tag_id,
          };
          this.dashbord.push(newItem);
          console.warn("No data : " + this.list5[i].tag_address);
          break;
        }
      }
    }
    console.warn(this.dashbord);
  },
};
</script>
