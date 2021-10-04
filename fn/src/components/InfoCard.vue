<template>
  <q-card class="col-4 rounded-borders-10 shadow-5" id="my-card-1">
        <q-card-section >
        <div class="text-h6 text-blue-8">Name : {{fname+' '+lname}}</div>
        <div class="text-subtitle2">Phone : {{ tel }}</div>
        <div class="text-subtitle2">ID civilization : {{id_civiliz}}</div>
      </q-card-section>
       <q-card-section>
         <div class="text-subtitle3">Type : {{category}}</div>
        <div class="text-subtitle3">Contact person : {{contract}}</div>
      </q-card-section>
      
      </q-card>
</template>

<script>
export default {
    props: ['fname','lname','tel','category','id_civiliz','contract','timeout'],
}
</script>

<style>

</style>