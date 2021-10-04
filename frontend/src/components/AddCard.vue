<template>
  <q-card class="my-card bg-indigo-1 rounded-borders-20 shadow-20 q-ma-sm">
    <q-card-section class="text-primary">
      <div class="row items-center no-wrap">
        <div class="col">
          <div class="text-center">
            <q-avatar square size="130px"
              ><!--190px-->
              <q-icon
                name="fas fa-wifi"
                color="red-8"
                style="font-size: 5rem"
              />
            </q-avatar>
          </div>
          <div class="col">
            <div class="text-h5 text-center">Tag #{{ id }}</div>
            <div class="text-subtitle2 text-center">
              <q-badge color="red-8" label="Disconnected" />
            </div>
          </div>
        </div>
      </div>
    </q-card-section>
    <div class="text-center">
            <q-avatar square size="90px"
              ><!--190px-->
            </q-avatar>
          </div>
    <q-card-section class="text-primary">
      <div class="row items-center no-wrap">
        <div class="col-auto">
          <q-btn color="primary" round flat icon="more_vert">
            <q-menu cover auto-close>
              <q-list>
                <q-item :to="'/register/' + id" clickable class="text-center">
                  <q-item-section>Register</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>
        </div>
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  props: ["id"],
};
</script>

<style></style>
