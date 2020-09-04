<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col>
          <v-tabs v-model="tab" grow>
            <v-tab>Item 1</v-tab>
            <v-tab>Item 2</v-tab>
            <v-tab>Item 3</v-tab>
          </v-tabs>

          <v-row>
            <v-col
              class="justify-space-between"
              v-for="edge in $page.events.edges"
              :key="edge.node.id"
            >
              <v-card class="mt-5">
                <v-img
                  class="white--text align-end"
                  height="200px"
                  :src="`http://localhost:1337${edge.node.thumbnail}`"
                >
                  <v-card-title> {{ edge.node.title }} </v-card-title>
                </v-img>
                <v-card-subtitle class="pb-0">{{
                  edge.node.date
                }}</v-card-subtitle>

                <v-card-actions>
                  <v-btn color="orange" text>More Info</v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<page-query>
query {
  events: allEvent {
    totalCount
    edges {
      node {
        id
        title
        date
        description
        price
        duration
        thumbnail
        image
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: "Hello, world!"
  },
  data() {
    return {
      tab: 0
    };
  },
  watch: {
    tab(val) {
      if (this.tab === 0) {
        this.showAllEvents();
      } else {
        this.showEventsByType();
      }
    }
  },
  methods: {
    showAllEvents() {
      console.log("all");
    },
    showEventsByType() {
      console.log("type");
    }
  }
};
</script>

<style></style>
