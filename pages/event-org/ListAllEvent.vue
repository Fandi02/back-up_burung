<template>
  <v-container id="regular-tables" fluid tag="section">
    <section class="mb-12 text-center">
      <h1 class="font-weight-light mb-2 headline" v-text="`Daftar Event`" />

      <span class="font-weight-light subtitle-1"> Table Daftar Event </span>
    </section>
    <div class="py-3" />

    <material-card
      color="success"
      dark
      icon="mdi-clipboard-plus"
      title="Table Daftar Event"
      class="px-5 py-3"
    >
      <v-simple-table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Tanggal</th>
            <th class="text-center">Lokasi</th>
            <th class="text-center">Pendaftar</th>
            <th class="text-right">Action</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(data, index) in listEvent" :key="index" :data="data">
            <td>{{ data.id }}</td>
            <td>{{ data.judul }}</td>
            <td>{{ data.jadwal }}</td>
            <td>{{ data.jml_tiket }}</td>
            <td class="text-center">
              <span class="red--text">{{ data.pendaftar }}</span
              >/<span class="green--text">{{ data.jumlahKursi }}</span>
            </td>
            <td class="text-right">
              <v-menu
                transition="slide-x-transition"
                bottom
                right
                :offset-y="offset"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    class="grey"
                    color="primary"
                    dark
                    v-bind="attrs"
                    v-on="on"
                  >
                    ...
                  </v-btn>
                </template>

                <v-list>
                  <v-list-item :to="`/event-org/detail-event/${data.id}`">
                    <v-list-item-title>Detail</v-list-item-title>
                  </v-list-item>

                  <v-list-item :to="`/event-org/EditEvent/${data.id}`">
                    <v-list-item-title>Edit</v-list-item-title>
                  </v-list-item>

                  <v-list-item @click="DeleteUser(data.id, index)">
                    <v-list-item-title>Cancel</v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
            </td>
          </tr>
        </tbody>
      </v-simple-table>
    </material-card>
  </v-container>
</template>
<script>
import MaterialCard from "../../components/Card/MaterialCard.vue";

export default {
  layout: "EoLayout",
  name: "ListUser",
  components: {
    MaterialCard,
  },

  data() {
    return {
      // listEvent: [
      //   {
      //     id: 1,
      //     judul: "Event 1",
      //     nomorTiket: "20220516-321-111",
      //     tanggal: "23 Oktober 2022",
      //     lokasi: "Bandung",
      //     pendaftar: 14,
      //     jumlahKursi: 24,
      //   },
      //   {
      //     id: 2,
      //     judul: "Event 2",
      //     nomorTiket: "20220516-321-112",
      //     tanggal: "23 Oktober 2022",
      //     lokasi: "Bandung",
      //     pendaftar: 20,
      //     jumlahKursi: 36,
      //   },
      //   {
      //     id: 3,
      //     judul: "Event 3",
      //     nomorTiket: "20220516-321-113",
      //     tanggal: "23 Oktober 2022",
      //     lokasi: "Bandung",
      //     pendaftar: 9,
      //     jumlahKursi: 25,
      //   },
      // ],
      offset: true,
      dialog3: false,

      listEvent: [],
    };
  },

  async fetch() {
    await this.$axios.get("/event").then((res) => (this.listEvent = res.data));
  },

  methods: {
    async search() {
      try {
        // await this.$axios
        //   .get("/search/?q=" + this.location)
        //   .then((res) => (this.datas = res.data.results));
      } catch (e) {
        this.error = e.response.data.message;
      }
    },
    async DeleteUser(id, index) {
      if (confirm("Do you really want to delete?")) {
        await this.$axios.delete("/event/delete/" + id);
        window.location.reload(true).catch((error) => {
          console.log(error);
        });
      }
    },
  },
};
</script>
