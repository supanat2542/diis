<template>
  <q-page class="q-pa-sm">
    <section-header
      title="Report"
      subTitle="แสดงข้อมูลการใช้งานของ Users"
    ></section-header>
    <q-tabs v-model="tab" class="q-mb-lg">
      <q-tab class="text-purple" name="Dairy" label="Dairy" />
      <q-tab class="text-orange" name="Monthly" label="Monthly" />
      <q-tab class="text-teal" name="Select Date" label="Select Date" />
    </q-tabs>
    <q-tab-panels
      v-model="tab"
      animated
      transition-prev="fade"
      transition-next="fade"
      style="background-color: #eceff1"
    >
      <q-tab-panel name="Dairy">
        <div class="q-pa-md">
          <q-table
            title="Timeline - Dairy 18/03/2021"
            :data="data"
            :columns="columns"
            row-key="name"
            class="rounded-borders-10 shadow-5"
          >
            <template v-slot:header="props">
              <q-tr :props="props">
                <q-th auto-width />
                <q-th v-for="col in props.cols" :key="col.name" :props="props">
                  {{ col.label }}
                </q-th>
              </q-tr>
            </template>

            <template v-slot:body="props">
              <q-tr :props="props">
                <q-td auto-width>
                  <q-btn
                    size="md"
                    color="primary-gradient"
                    round
                    to="/timeline"
                    :icon="props.expand ? '' : 'person_pin_circle'"
                  />
                </q-td>
                <q-td v-for="col in props.cols" :key="col.name" :props="props">
                  {{ col.value }}
                </q-td>
              </q-tr>
            </template>
          </q-table>
        </div>
      </q-tab-panel>

      <q-tab-panel name="Monthly">
        <div class="q-pa-md">
          <q-table
            title="Timeline - Monthry 03/2021"
            :data="data"
            :columns="columns"
            row-key="name"
            class="rounded-borders-10 shadow-5"
          >
            <template v-slot:header="props">
              <q-tr :props="props">
                <q-th auto-width />
                <q-th v-for="col in props.cols" :key="col.name" :props="props">
                  {{ col.label }}
                </q-th>
              </q-tr>
            </template>

            <template v-slot:body="props">
              <q-tr :props="props">
                <q-td auto-width>
                  <q-btn
                    size="md"
                    color="primary-gradient"
                    round
                    to="/timeline"
                    :icon="props.expand ? '' : 'person_pin_circle'"
                  />
                </q-td>
                <q-td v-for="col in props.cols" :key="col.name" :props="props">
                  {{ col.value }}
                </q-td>
              </q-tr>
            </template>
          </q-table>
        </div>
      </q-tab-panel>

      <q-tab-panel name="Select Date">
        <div class="row-12">
          <div class="row-4">Select Date</div>
          <div class="q-pa-md" style="max-width: 300px">
            <q-input filled v-model="date" mask="date" :rules="['date']">
              <template v-slot:append>
                <q-icon name="event" class="cursor-pointer">
                  <q-popup-proxy
                    ref="qDateProxy"
                    transition-show="scale"
                    transition-hide="scale"
                  >
                    <q-date v-model="date">
                      <div class="row items-center justify-end">
                        <q-btn
                          v-close-popup
                          label="Close"
                          color="primary"
                          flat
                        />
                      </div>
                    </q-date>
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
          </div>
        </div>

        <div class="q-pa-md">
          <q-table
            title="Timeline - Date 18/03/2021"
            :data="data"
            :columns="columns"
            row-key="name"
            class="rounded-borders-10 shadow-5"
          >
            <template v-slot:header="props">
              <q-tr :props="props">
                <q-th auto-width />
                <q-th v-for="col in props.cols" :key="col.name" :props="props">
                  {{ col.label }}
                </q-th>
              </q-tr>
            </template>
            <template v-slot:body="props">
              <q-tr :props="props">
                <q-td auto-width>
                  <q-btn
                    size="md"
                    color="primary-gradient"
                    round
                    to="/timeline"
                    :icon="props.expand ? '' : 'person_pin_circle'"
                  />
                </q-td>
                <q-td v-for="col in props.cols" :key="col.name" :props="props">
                  {{ col.value }}
                </q-td>
              </q-tr>
            </template>
          </q-table>
        </div>
      </q-tab-panel>
    </q-tab-panels>
  </q-page>
</template>

<script>
import SectionHeader from "../components/SectionHeader.vue";

export default {
  components: {
    SectionHeader,
  },
  data() {
    return {
      tab: "Dairy",
      date: "2021/03/18",
      columns: [
        {
          name: "name",
          required: true,
          label: "Name",
          align: "left",
          field: (row) => row.name,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "date",
          align: "center",
          label: "Date",
          field: "date",
          sortable: true,
        },
        {
          name: "time-start",
          align: "center",
          label: "Time Start",
          field: "timeStart",
          sortable: true,
        },
        {
          name: "time-stop",
          align: "center",
          label: "Time Stop",
          field: "timeStop",
          sortable: true,
        },
        {
          name: "type",
          align: "center",
          label: "Type",
          field: "type",
          sortable: true,
        },
        {
          name: "location",
          align: "center",
          label: "Location",
          field: "location",
          sortable: true,
        },
      ],

      data: [
        {
          name: "Harry Home",
          date: "03/18/2021",
          timeStart: "8.30",
          timeStop: "11.00",
          type: "Electrician",
          location: "1202A",
          // timeline: 11
        },
        {
          name: "Oliver Home",
          date: "03/18/2021",
          timeStart: "11.30",
          timeStop: "13.20",
          type: "Electrician",
          location: "1202A",
          // timeline: 54
        },
        {
          name: "Jack Home",
          date: "03/18/2021",
          timeStart: "14.30",
          timeStop: "15.00",
          type: "Electrician",
          location: "1302A",
          // timeline: 54
        },
        {
          name: "Alfie Home",
          date: "03/18/2021",
          timeStart: "15.28",
          timeStop: "16.30",
          type: "Electrician",
          location: "1402A",
          // timeline: 54
        },
        {
          name: "Harry Home",
          date: "03/18/2021",
          timeStart: "8.30",
          timeStop: "11.00",
          type: "Electrician",
          location: "1202A",
          // timeline: 11
        },
        {
          name: "Oliver Home",
          date: "03/18/2021",
          timeStart: "11.30",
          timeStop: "13.20",
          type: "Electrician",
          location: "1202A",
          // timeline: 54
        },
        {
          name: "Jack Home",
          date: "03/18/2021",
          timeStart: "14.30",
          timeStop: "15.00",
          type: "Electrician",
          location: "1302A",
          // timeline: 54
        },
        {
          name: "Alfie Home",
          date: "03/18/2021",
          timeStart: "15.28",
          timeStop: "16.30",
          type: "Electrician",
          location: "1402A",
          // timeline: 54
        },
      ],
    };
  },
};
</script>

<style lang="sass">
.my-sticky-header-table
  /* height or max-height is important */
  height: 490px

  .q-table__top,
  .q-table__bottom,
  thead tr:first-child th
    /* bg color is important for th; just specify one */
    background-color: #c1f4cd

  thead tr th
    position: sticky
    z-index: 1
  thead tr:first-child th
    top: 0

  /* this is when the loading indicator appears */
  &.q-table--loading thead tr:last-child th
    /* height of all previous header rows */
    top: 48px
</style>
