<template>
  <div>
    <v-card dark class="ma-2">
      <v-container>
        <v-row>
          <v-col cols="2">
            <v-list-item-avatar
              tile
              size="80"
              color="grey"
            ></v-list-item-avatar>
          </v-col>
          <v-col cols="10">
            <v-list-item-title class="text-h5 mb-1">
              {{ data.judul }}
            </v-list-item-title>
            <v-row>
              <v-col cols="6">
                <v-list-item-subtitle>Tanggal</v-list-item-subtitle>
                <v-list-item-subtitle>Lokasi</v-list-item-subtitle>
                <v-list-item-subtitle>Biaya</v-list-item-subtitle>
              </v-col>
              <v-col cols="6">
                <v-list-item-subtitle>{{ data.tanggal }} / {{data.jam}}</v-list-item-subtitle>
                <v-list-item-subtitle>{{
                  data.kota
                }}</v-list-item-subtitle>
                <v-list-item-subtitle>{{
                  data.harga_tiket
                }}</v-list-item-subtitle>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-container>

      <v-card-actions class="justify-center">
        <nuxt-link
          style="text-decoration: none; color: inherit"
          :to="'/user/detail-event/' + data.event_id"
        >
          <v-btn color="orange" text> Detail </v-btn>
        </nuxt-link>

        <nuxt-link
          style="text-decoration: none; color: inherit"
          :to="'/user/booking/' + data.event_id"
        >
          <v-btn color="orange" text> Booking </v-btn>
        </nuxt-link>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
    },
  },
};
</script>