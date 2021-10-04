<template>
<div>

  <q-icon
    name="fas fa-user-tag"
    class="tag blink row q-gutter-xs"
    color="orange-8"
    size="30px"
  >
    <q-popup-proxy>
      <Map-card
        :id_visitor="id_visitor"
        :id="id"
        :fname="fname"
        :lname="lname"
        :tel="tel"
        :category="category"
        :room="room"
        :contract="contract"
        :timeout="time_out"
      ></Map-card>
    </q-popup-proxy>
    
     <q-badge color="green-8" :label="'TAG '+id"  />
     <q-icon v-if="this.showing==true" class="warning text-red-9" name="warning_amber" />
  </q-icon>
  
  </div>
</template>

<script>
import MapCard from "../components/MapCard.vue";
const moment = require("moment");
export default {
  props: [
    "id_visitor",
    "id",
    "fname",
    "lname",
    "tel",
    "category",
    "room",
    "contract",
    "timestamp",
  ],
  components: {
    MapCard,
  },
  data() {
    return {
      showing: false,
      time_out:""
    };
  },
  mounted() {
    console.warn(this.timestamp+" == "+moment().format())
    var now = moment().format()
    var last = this.timestamp
    var now_time = moment(now)
    var last_time = moment(last)
    var time_out =now_time.diff(last_time, 'hours')
    console.warn("Time Out : "+time_out)
    if(time_out==0){
      this.time_out="0"
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
    console.warn(this.showing)
  },
};
</script>

<style>
.tag {
  width: 50px;
}
.blink {
  animation: blinker 5s linear infinite;
}
.warning {
  position: absolute;
  overflow: hidden;
}
@keyframes blinker {
  50% {
    opacity: 0;
  }
}
</style>