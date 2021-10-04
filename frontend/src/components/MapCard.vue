<template>
  <q-card class="my-card">
    <q-card-section class="text-primary">
      <div class="row items-center no-wrap">
        <div class="col">
        <div class="text-center">
        <q-avatar square size="80px">
          <q-icon name="fas fa-user-tag" color="orange-8" />
        </q-avatar>
      </div>    
        </div> 
        <div class="col">
          <div class="text-h6">Guest #{{ id }}</div>
          <div class="text-subtitle2 q-gutter-xs ">
            <q-badge color="green-8" class="justify-center" :label="room" />
            <q-badge v-if="this.timeout!=0" color="yellow-8" text-color="black" class="justify-center">
            <q-icon
              name="warning"
              size="14px"
              class="q-ml-xs"
            />
             {{this.timeout}}
          </q-badge>
          </div>
        </div>

        <div class="col-auto">
          <q-btn color="primary" round flat icon="more_vert">
            <q-menu cover auto-close>
              <q-list>
                <q-item :to="'/timeline/'+id_visitor" clickable>
                  <q-item-section >Check TimeLine</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>
        </div>
      </div>
    </q-card-section>

    <q-card-section class="q-pt-none text-primary">
      <q-list separator>
        <q-item v-ripple>
          <q-item-section>
            <q-item-label overline>Name</q-item-label>
            <q-item-label>{{fname+' '+lname}}</q-item-label>
          </q-item-section>
        </q-item>
        <q-item v-ripple>
          <q-item-section>
            <q-item-label overline>Tel no.</q-item-label>
            <q-item-label>{{tel}}</q-item-label>
          </q-item-section>
        </q-item>
        <q-item v-ripple>
          <q-item-section>
            <q-item-label overline>Category</q-item-label>
            <q-item-label>{{category}}</q-item-label>
          </q-item-section>
        </q-item>
        <q-item v-ripple>
          <q-item-section>
            <q-item-label overline>Contact Person</q-item-label>
            <q-item-label>{{ contract }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-card-section>
    
  </q-card>
  
  
</template>

<script>
export default {
  props: ['id_visitor','id','fname','lname','tel','category','room','contract','timeout'],
  
};
  
</script>

<style>
</style>