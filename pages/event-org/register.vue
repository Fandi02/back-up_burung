<template>
  <v-row align="center" justify="center">
    <v-col cols="12" sm="12" md="12">
      <v-card light class="pa-5 ma-5">
        <v-form
          ref="form"
          v-model="valid"
          lazy-validation
          @submit.prevent="register"
        >
          <img src="/logo.png" alt="Kontes Burung Logo" class="center" />
          <h2 class="text-center mt-4">Daftar Akun Event-Organizer</h2>
          <v-row justify="center">
            <v-col md="12" justify="center" class="text-center">
              <v-text-field
                v-model="name"
                :counter="25"
                :rules="nameRules"
                label="Nama"
                required
              ></v-text-field>

              <v-text-field
                v-model="phone"
                label="No Telephone"
                required
              ></v-text-field>

              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
                required
              ></v-text-field>

              <v-text-field
                v-model="password"
                :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                :rules="passwordRules"
                :type="show ? 'text' : 'password'"
                name="input-10-1"
                label="Password"
                hint="At least 8 characters"
                counter
                @click:append="show = !show"
              ></v-text-field>

              <v-card-actions class="justify-center">
                <v-btn type="submit" color="primary" class="mr-4">
                  Register
                </v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-form>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: "",
    nameRules: [
      (v) => !!v || "Name tidak boleh kosong",
      (v) => (v && v.length <= 25) || "Name harus kurang dari 25 huruf",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail tidak boleh kosong",
      (v) => /.+@.+\..+/.test(v) || "Format e-mail tidak sesuai",
    ],
    password: "",
    passwordRules: [
      (v) => !!v || "Password tidak boleh kosong.",
      (v) => v.length >= 8 || "Password minimal 8 huruf",
    ],
    phone: "",
    show: false,
  }),

  methods: {
    async register() {
      try {
        await this.$axios.post("/eo/register", {
          no_hp: this.phone,
          email: this.email,
          password: this.password,
          nama: this.name,
        });
        this.$router.push("/event-org");
      } catch (e) {
        this.error = e.response.data.message;
      }
    },
  },
};
</script>