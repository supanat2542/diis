<template>
  <q-page class="q-pa-sm">
    <!-------------------------- From Register ---------------------------------------- -->
    <section-header
      title="Register"
      subTitle="การลงทะเบียน Tag"
    ></section-header>
    <div class="row q-gutter-col-md justify-center">
      <div class="col-9">
        <q-card
          class="my-card bg-indigo-1 rounded-borders-20 shadow-20 q-ma-sm"
        >
          <q-card-section class="text-primary">
            <div class="row items-center no-wrap">
              <div class="col-3">
                <div class="text-center">
                  <q-avatar square size="150px">
                    <q-icon name="fas fa-user-tag" color="orange-8" />
                  </q-avatar>
                </div>
              </div>
              <div class="col-7">
                <div class="text-h3">Tag {{ id }}</div>
                <div class="text-subtitle2">
                  <q-badge color="red-8" label="Disconnected" />
                </div>
              </div>
            </div>
          </q-card-section>
          <q-card-section style="margin: 30px">
            <!-- -------------- form ----------------------------- -->
            <form
              @submit.prevent.stop="onSubmit"
              @reset.prevent.stop="onReset"
              method="post"
            >
              <div class="row">
                <div class="col-2">Name</div>
                <div class="col-4">
                  <q-input
                    type="text"
                    name="first name"
                    v-model="posts.first_name"
                    label="Fist Name"
                    lazy-rules
                    maxlength="15"
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'Please enter your first name',
                    ]"
                  />
                </div>
                <div class="col-4">
                  <q-input
                    name="last name"
                    v-model="posts.last_name"
                    label="Last Name"
                    lazy-rules
                    maxlength="15"
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'Please enter your last name',
                    ]"
                  />
                </div>
              </div>
              <div class="row" id_civiliz="top">
                <div class="col-2">tel</div>
                <div class="col-8">
                  <q-input
                    type="text"
                    v-model="posts.tel"
                    label="Number tel"
                    mask="### - #######"
                    lazy-rules
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'Please type your number tel',
                      (val) =>
                        val.length >= 13 || 'Please enter your real number tel',
                    ]"
                  />
                </div>
              </div>
              <div class="row" id_civiliz="top">
                <div class="col-2">id card number</div>
                <div class="col-8">
                  <q-input
                    type="text"
                    v-model="posts.id_civiliz"
                    label="x-xxxx-xxxxx-xx-x"
                    mask="# - #### - ##### - ## - #"
                    lazy-rules
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'Please enter your 13 Identification Number',
                      (val) =>
                        val.length >= 25 ||
                        'Please enter your real Identification Number',
                    ]"
                  />
                </div>
              </div>
              <div class="row" id_civiliz="top">
                <div class="col-2">Person Contract</div>
                <div class="col-8">
                  <q-input
                    v-model="posts.Person"
                    label="Person Contract"
                    lazy-rules
                    maxlength="20"
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'Please enter your person contract',
                    ]"
                  />
                </div>
              </div>
              <div class="row" id_civiliz="top">
                <div class="col-2">category</div>
                <div class="col-8">
                  <q-input
                    v-model="posts.category"
                    label="category to contract"
                    lazy-rules
                    maxlength="20"
                    :rules="[
                      (val) =>
                        (val && val.length > 0) || 'Please enter your category',
                    ]"
                  />
                </div>
              </div>
              <div class="row justify-end" id_civiliz="topper">
                <div class="col-3">
                  <!-------------------------- Button Add Data ---------------------------------------- -->
                  <q-btn
                    icon="check"
                    color="primary-gradient"
                     label="Submit" type="submit"
                    clickable
                  />
                  <q-btn
                    icon="refresh"
                    label="Reset"
                  type="reset"
                    color="primary"
                    flat
                    class="q-ml-sm"
                  ></q-btn>
                </div>
              </div>
            </form>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
import SectionHeader from "../components/SectionHeader.vue";
import DeviceCard from "../components/DeviceCard.vue";
import AddCard from "../components/AddCard.vue";
import { axios } from "boot/axios";
export default {
  name: "PageIndex",
  components: {
    SectionHeader,
    DeviceCard,
    AddCard,
  },
  data() {
    return {
      posts: {
        first_name: "",
        last_name: "",
        tel: "",
        category: "",
        id_civiliz: "",
        Location: null,
        Person: "",
        taguse_address: "",
        visitor_id: "",
      },
      id: this.$route.params.id,
      list: undefined,
    };
  },
  async mounted() {
    //<------------------------- Connect Database ------------------------------------- -->
    const url = "http://localhost:3030/api/" 
    let resp = await axios.get(url+"visitors");
    this.count = resp.data.result.rows.length;
    this.list = resp.data.result.rows;
    console.warn(this.list);
    // console.warn("id last "+this.list[this.count - 1].visitor_id + 1);
    this.posts.visitor_id = this.list[this.count - 1].visitor_id + 1;
    let resp2 = await axios.get(url+"tags");
    this.list2 = resp2.data.result.rows;
    console.warn(this.list2);
    for (var i = 0; i < this.list2.length; i++) {
      if (this.list2[i].tag_id == this.id) {
        this.taguse_address = this.list2[i].tag_address;
        console.warn("id address : " + this.taguse_address);
        break;
      }
    }
    console.warn("tag id : "+this.taguse_address);
  },
  methods: {
    //<------------------------- Fuction Add Data ------------------------------------------ -->
    async onSubmit() {
      // console.warn(" 1 : "+this.posts.first_name + " 2 : "+this.posts.last_name + " 3 : "+this.posts.tel + " 4 : "+this.posts.category +" 5 : "+ this.posts.id_civiliz  +" 6 : "+ this.posts.Person + " 7 : "+ this.posts.tel.length)
      if (
        this.posts.first_name !== "" &&
        this.posts.last_name !== "" &&
        this.posts.tel !== "" &&
        this.posts.category !== "" &&
        this.posts.id_civiliz !== "" &&
        this.posts.Person !== "" &&
        this.posts.tel.length == 13 &&
        this.posts.id_civiliz.length == 25
      ) {
        console.warn("connect");
        console.warn(this.posts);
        const url = "http://localhost:3030/api/" 
        let result = await axios.post(url+"visitors", [
          {
            tag_address: this.taguse_address,
            first_name: this.posts.first_name,
            last_name: this.posts.last_name,
            tel: this.posts.tel,
            category: this.posts.category,
            id_civiliz: this.posts.id_civiliz,
            contract: this.posts.Person,
          },
        ]);
        console.warn(result);
        let result2 = await axios.post(url+"scanlog", [
          {
            device_address: this.taguse_address,
            scanner_id: "8e61a75d-12b7-4bda-8bc1-ed5983d33408-003",
          },
        ]);
        console.warn(result2);
        this.$router.push("/index");
      } else {
        console.warn("Not connect");
         alert("Please inform your information before submit.");
      }
    },
    onReset () {
      this.posts.first_name = null;
      this.posts.last_name = null;
      this.posts.tel = null;
      this.posts.category = null;
      this.posts.id_civiliz = null;
      this.posts.Person = null;
    }
  },
};
</script>

<style>
#top {
  margin-top: 10px;
}
#topper {
  margin-top: 50px;
  margin-bottom: 30px;
}
</style>