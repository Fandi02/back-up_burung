<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="12" sm="12" md="12">
          <v-card>
            <v-card-text class="text-center">
              <div
                class="
                  display-2
                  font-weight-light
                  col col-12
                  text--primary
                  pa-0
                  mb-8
                "
              >
                <h5 class="font-weight-light">Edit Bird Type</h5>
              </div>
              <v-row class="text-left">
                <v-col cols="12">
                  <form @submit.prevent="submit" ref="form">
                    <v-row>
                      <v-col cols="12">
                        <v-text-field
                          v-model="datas.nama"
                          :counter="25"
                          label="Nama Burung"
                          required
                          filled
                        ></v-text-field>
                      </v-col>
                    </v-row>
                    <v-card-actions class="justify-center">
                      <v-btn color="orange" text @click="clear"> Clear </v-btn>

                      <v-btn color="orange" type="submit" text> Submit </v-btn>
                    </v-card-actions>
                  </form>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  layout: "EoLayout",
  components: {
    },
  data: () => ({
    datas: {
      type: Object,
    },
    birdName: ""
  }),

  async fetch() {
    await this.$axios
      .get("/jenisBurung/" + this.$route.params.edit)
      .then((res) => (this.datas = res.data))
  },

  methods: {
    clear() {
      this.$refs.form.reset();
    },
    async submit() {
      try {
        await this.$axios.put("/jenisBurung/update/" + this.$route.params.edit, {
          nama: this.datas.nama,
        });
        this.$router.push("/event-org/birdtype");
      } catch (e) {
        this.error = e.response;
        console.log(this.error);
      }
    },
  },
};
</script>
