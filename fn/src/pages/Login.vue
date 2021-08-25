<template>
  <q-layout view="hHh Lpr lFf">
    <q-page-container class="bg-grey-2">
      <q-page padding class="row items-center justify-center">
        <div class="row full-width">
          <div class="col-md-8 offset-md-2 col-xs-12 q-pl-md q-pr-md q-pt-sm">
            <q-card flat class="bg-white text-black">
              <div class="row">
                <div class="col-md-6 col-xs-12 q-pa-md">
                  <q-img
                    placeholder-src="~assets/loginpage.png"
                    src="~assets/loginpage.png"
                    spinner-color="white"
                  ></q-img>
                </div>

                <div class="col-md-6 col-xs-12">
                  <div class="q-pa-md">
                    <div
                      class="text-h6 q-pb-md text-blue-8 text-center text-weight-bolder"
                    >
                      Login
                    </div>
                    <q-form
                      @submit="onSubmit"
                      @reset="onReset"
                      class="q-gutter-md"
                    >
                      <q-input
                        filled
                        v-model="name"
                        label="Username"
                        lazy-rules
                        :rules="[
                          (val) =>
                            (val && val.length > 0) || 'Please type Username',
                        ]"
                      />

                      <q-input
                        filled
                        type="password"
                        v-model="password"
                        label="Password"
                        lazy-rules
                        :rules="[
                          (val) =>
                            (val !== null && val !== '') ||
                            'Please type your password',
                        ]"
                      />

                      <div>
                        <q-btn
                          label="submit"
                          type="submit"
                          color="primary"
                          @click="onSubmit()"
                        />
                        <q-btn
                          label="Reset"
                          type="reset"
                          color="primary"
                          flat
                          class="q-ml-sm"
                        />
                      </div>
                    </q-form>
                  </div>
                </div>
              </div>
            </q-card>
          </div>
        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>



// <script>
export default {
  data() {
    return {
      name: null,
      password: null,
    };
  },

  methods: {
    onSubmit() {
      if (this.name == "admin" && this.password == "admin") {
        console.warn("click submit");
        this.$router.push("/index");
      }
      
    },
    onReset() {
      this.name = null;
      this.password = null;
    },
    onReset() {
      this.name = null;
      this.password = null;
    },
  },
};
</script>

