<template>
  <v-container>
    <v-row>
      <v-col v-for="(model, index) in models" :key="index" cols="12" sm="4">
        <v-card elevation="3" class="mx-auto" max-width="400">
          <v-img
            class="white--text align-end"
            height="200px"
            src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
          >
            <v-card-title>{{ model.title }}</v-card-title>
          </v-img>
          <v-card-subtitle class="pb-0"> Number 10 </v-card-subtitle>

          <v-card-text class="text--primary">
            <div>Whitehaven Beach</div>

            <div>Whitsunday Island, Whitsunday Islands</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="orange" text> More </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <v-btn @click="checkConnect">Click ME</v-btn>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    models: [{ title: "HardMSEG" }, { title: "PraNet" }, { title: "ResNet" }],
    loading: false,
  }),
  methods: {
    async checkConnect(event) {
      this.loading = true
      try {
        const res = await this.$axios.$get(`${process.env.apiBaseUrl}/`)
        console.log(res)
        
        this.loading = false
      } catch (error) {
        this.loading = false
      }
    }
  }
};
</script>