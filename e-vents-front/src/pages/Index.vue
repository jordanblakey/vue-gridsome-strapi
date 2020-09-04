<template>
  <Layout v-slot="{ searchText }">
    <v-tabs v-model="tab" grow>
      <v-tab>All Events</v-tab>
      <v-tab>Coding</v-tab>
      <v-tab>Knitting</v-tab>
    </v-tabs>

    <v-row>
      <v-col
        class="justify-space-between"
        v-for="edge in getEvents(searchText)"
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
            formatDate(edge.node.date)
          }}</v-card-subtitle>

          <v-card-actions>
            <g-link :to="`/events/${edge.node.id}`">
              <v-btn color="orange" text>More Info</v-btn>
            </g-link>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
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
        category
      }
    }
  }
}
</page-query>

<script>
import moment from "moment";
export default {
  metaInfo: {
    title: "Hello, world!"
  },
  data() {
    return {
      tab: 0,
      events: []
    };
  },
  mounted() {
    this.events = this.$page.events.edges;
  },
  watch: {
    tab(val) {
      if (this.tab === 0) {
        this.showAllEvents();
      } else {
        this.showEventsByType(val);
      }
    }
  },
  methods: {
    showAllEvents() {
      this.events = this.$page.events.edges;
    },
    showEventsByType(val) {
      this.events = this.$page.events.edges.filter(edge => {
        return edge.node.category === val;
      });
    },
    formatDate(date) {
      return moment(date).format("MMMM Do YYYY, h:mm a");
    },
    getEvents(searchText) {
      return this.events.filter(edge => {
        return edge.node.title.toLowerCase().includes(searchText.toLowerCase());
      });
    }
  }
};
</script>

<style>
.v-card__actions a {
  text-decoration: none;
}
</style>
