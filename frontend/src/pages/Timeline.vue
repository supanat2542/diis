<template>
  <q-page class="q-pa-sm">
    <section-header
      title="Time Line"
      subTitle="แสดงข้อมูลการใช้งานของ User"
    ></section-header>
    <!-------------------------- Infomation User ------------------------------------>
    <q-layout view="hHh Lpr lFf">
      <q-page-container class="bg-grey-2">
              <div v-for="itemz in list" :key="itemz.visitor_id" >
                <div v-if="itemz.visitor_id == id" class="row justify-center" >
                
                  <div class="col-md-8 col-xs-12 q-pa-md " >
                    <info-card
                      class="col-4"
                      :fname="itemz.first_name"
                      :lname="itemz.last_name"
                      :tel="itemz.tel"
                      :id_civiliz="itemz.id_civiliz"
                      :category="itemz.category"
                      :contract="itemz.contract"
                    />
                  </div>         
                    <div class="col-md-3 col-xs-12 q-pa-md text-blue-8" >
                        <q-card
                          class="col-3 rounded-borders-10 shadow-5 text-center"
                          id="my-card-2" 
                        >
                          <q-img height="auto" width="150px" 
                            placeholder-src="~assets/timeline.png"
                            src="~assets/timeline.png"
                            spinner-color="white"
                          ></q-img>

                          <q-card-section class="text-h5 text-center">
                            <div>Tag {{ itemz.tag_id }}</div>
                          </q-card-section>
                        </q-card>
                  
                    </div>
              
                </div>
              </div>
             

        <!--------------------------- Timeline User ------------------------------------>
        <q-timeline color="secondary" style="padding-left: 4rem " >
          <q-timeline-entry heading> Timeline 
            <div v-if="this.showing==true"class="text-subtitle1 text-yellow-9 row">
               <q-icon name="warning" size="30px"/>
               <p> Time out {{time_out}} </p>
            </div>
          </q-timeline-entry>
                

          <q-timeline-entry
            v-for="time in timeline"
            :key="time.time"
            :title="'Room : ' + time[time.length - 2]"
            :subtitle="time[time.length - 1]"
          >
            Time : {{ time[time.length - 3] }} - {{ time[0] }}
          </q-timeline-entry>
          <q-timeline-entry title=" Start " subtitle=" " icon="watch_later">
          </q-timeline-entry>
        </q-timeline>
        <!---------------------------close Timeline User ------------------------------------>
      </q-page-container>
   </q-layout>
  </q-page>
</template>

<script>
import SectionHeader from "../components/SectionHeader.vue";
import InfoCard from "../components/InfoCard.vue";
import { axios } from "boot/axios";
const moment = require("moment");
export default {
  components: {
    SectionHeader,
    InfoCard,
  },
  data() {
    return {
      id: this.$route.params.id,
      timeline: [],
      time: [],
      list: undefined,
      list2: undefined,
      tag: undefined,
      showing: false,
      time_out:""
    };
  },
  async mounted() {
    // setTimeout(function () {
    //   location.reload(1);
    // }, 60000);
    //<------------------------- Connect Database ----------------------------------------------------------->
    // const url = "http://localhost:3030/api/";
    const url = "http://localhost:3030/api/";
    let resp1 = await axios.get(url + "visitors");
    this.list = resp1.data.result.rows;
    console.warn("list item visitors");
    console.warn(this.list);
    for (var j = 0; j < this.list.length; j++) {
      if (this.id == this.list[j].visitor_id) {
        break;
      }
    }
    console.warn(" j : " + j);
    let resp2 = await axios.get(url + "selectlog", {
      params: {
        device_address: this.list[j].tag_address,
        time_start: moment(this.list[j].time_start).format(
          "YYYY-MM-DD hh:mm:ss A"
        ),
        time_stop: moment(this.list[j].time_stop).add(1, 'minute').format(
          "YYYY-MM-DD hh:mm:ss A"
        ),
      },
    });
    this.list2 = resp2.data.result.rows;
    console.warn("list2 scanerlog");
    console.warn(this.list2);
    //<------------------------- Create Timeline ----------------------------------->
    var rooms = this.list2[0].room;
    var times = moment(this.list2[0].scan_timestamp).format("hh:mm A")
    console.warn(moment(this.list2[0].scan_timestamp).format("hh:mm A"))
    if (this.list[j].time_stop == null) {
      this.time.push("In Use Now.");
    }
    for (var i = 0; i < this.list2.length; i++) {
      if (this.list2[i].room != rooms 
      // && moment(this.list2[i].scan_timestamp).format("hh:mm A") != times
      ) {
        this.time.push(this.list2[i - 1].room);
        this.time.push(
          moment(this.list2[i].scan_timestamp).format("YYYY-MM-DD")
        );
        this.timeline.push(this.time);
        this.time = [];
        rooms = this.list2[i].room;
        times = moment(this.list2[i].scan_timestamp).format("hh:mm A")
        --i;
      } else {
        this.time.push(moment(this.list2[i].scan_timestamp).format("hh:mm A"));
      }
    }
    this.time.push(this.list2[this.list2.length - 1].room);
    this.time.push(
      moment(this.list2[this.list2.length - 1].scan_timestamp).format(
        "YYYY-MM-DD"
      )
    );
    
    this.timeline.push(this.time);
    console.warn(this.timeline);
    // console.warn(10**(((-69)-(-85))/(10 * 2)))
    
    // for (var i = 0; i < this.list2.length; i++) {
      // console.warn(this.list2[i].room +" ==== "+rooms+" ---> "+i)
      // console.warn(moment(this.list2[i].scan_timestamp).format("hh:mm A") +" ==== "+ this.time[this.time.length-1]+" : "+i)
      //  if(moment(this.list2[i].scan_timestamp).format("hh:mm A")==this.time[this.time.length-1]&&this.list2[i].room!=rooms){
      //   console.warn("kanssssssssssssssssssssssssssssssssss")
      //   console.warn(this.list2[i-1].device_rssi+" // "+this.list2[i].device_rssi)
      //   var diis_1 = 10**(((-69)-(this.list2[i-1].device_rssi))/(10 * 2))
      //   var diis_2 = 10**(((-69)-(this.list2[i].device_rssi))/(10 * 2))
      //   console.warn(diis_1+" -- "+diis_2)
      //   if(diis_1>diis_2){
      //     console.warn("Beafore")
      //     console.warn(this.time)
      //     // this.time = [];
      //     console.warn("After")
      //     console.warn(this.time)
      //   }
      // } else 
      // if (this.list2[i].room != rooms && moment(this.list2[i].scan_timestamp).format("hh:mm A") != this.time[this.time.length-1]) {
      //   console.warn("Date : "+moment(this.list2[i].scan_timestamp).format("YYYY-MM-DD"))
      //   this.time.push(this.list2[i - 1].room);
      //   this.time.push(
      //     moment(this.list2[i].scan_timestamp).format("YYYY-MM-DD")
      //   );
      //   this.timeline.push(this.time);
      //   console.warn(this.time)
      //   this.time = [];
      //   rooms = this.list2[i].room;
      //   times = moment(this.list2[i].scan_timestamp).format("hh:mm A")
      //   --i;
      // } else if(this.list2[i].room != rooms && moment(this.list2[i].scan_timestamp).format("hh:mm A") == this.time[this.time.length-1]){
      //   console.warn("kanssssssssssssssssssssssssssss")
      //    console.warn(this.time)
      //    ++i
      // }else {
      //   this.time.push(moment(this.list2[i].scan_timestamp).format("hh:mm A"));
      //   console.warn(moment(this.list2[i].scan_timestamp).format("hh:mm A"))
      // }
      
    // }
     console.warn(this.list2[0].scan_timestamp+" == "+moment().format())
    var now = moment().format()
    var last = this.list2[0].scan_timestamp
    var now_time = moment(now)
    var last_time = moment(last)
    var time_out =now_time.diff(last_time, 'hours')
    console.warn("Time Out : "+time_out)
    if(this.timeline[0][0]!="In Use Now."){
      this.showing=false
    }else{
      if(time_out==0){
      this.time_out=""
      this.showing=false
    }else if(time_out==1){
      this.time_out="1 hr"
      this.showing=true
    }else if(time_out==2){
      this.time_out="2 hr"
      this.showing=true
    }else if(time_out>=3){
      this.time_out="more 3 hr"
      this.showing=true
    }
    }
    console.warn(this.showing)
  },
};
</script>

<style lang="sass" scoped>
#my-card-1
  height: 100%
  padding: 27px
#my-card-2
  padding: 30px
  height: 100%
#icon
  font-size: 9em
  display: inline-block
  width: 100%
</style>