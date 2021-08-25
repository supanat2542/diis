<template>
<div >
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
      ></Map-card>
    </q-popup-proxy>
     <q-badge color="green-8" :label="'TAG '+id"  />
  </q-icon>
  </div>
</template>

<script>
import MapCard from "../components/MapCard.vue";
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
  ],
  components: {
    MapCard,
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

@keyframes blinker {
  50% {
    opacity: 0;
  }
}
</style>