<template>
  <v-app>
    <v-main>
      <v-container>
        <h2>User Purchase Data</h2>
        <v-row>
          <v-col md="3">
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-data-table
              :headers="headers"
              :items="posts"
              :items-per-page="5"
              :search="search"
              class="elevation-1"
            >
            </v-data-table>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  props: ["posts"],
  data: () => ({
    search: "",
    headers: [
      { text: "Name", value: "name", sortable: false },
      { text: "Date", value: "Date" },
      // { text: "Product", value: "product", sortable: false },
      // { text: "Price", value: "price", sortable: false },
      { text: "Quantity", value: "quantity", sortable: false },
      { text: "Total revenue ", value: "total", sortable: false },
      { text: "Total Discont", value: "Discont", sortable: false }
    ]
  })
};
</script>