<template>
  <div class="home">
    <v-text-field
      v-model="page"
      hint="Broj stranice"
      :persistent-hint="true"
      @input="promjenaUlaza"
    ></v-text-field>

    <v-text-field
      v-model="perPage"
      hint="Redaka po stranici"
      :persistent-hint="true"
      @input="promjenaUlaza"
    ></v-text-field>

    <v-container>
      <v-row>
        <v-col
          cols="3"
          v-for="market in markets"
          :key="market.id"
        >
          <v-card class="mx-auto" max-width="344">
            <v-img :src="market.image" height="200px"></v-img>

            <v-card-title>{{ market.name }}</v-card-title>

            <v-card-subtitle
              ><a :href="market.url">{{ market.url }}</a></v-card-subtitle
            >

            <v-card-actions>
              <v-btn color="orange lighten-2" text> Detalji </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <!--
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: "Home",
  components: {
    // HelloWorld
  },
  data: () => {
    return {
      page: 1,
      perPage: 20,
      markets: [],
    };
  },
  created() {
    this.dohvatiPodatke();

    setTimeout(() => {
      this.dohvatiPodatke();
    }, 15000)
  },
  methods: {
    promjenaUlaza: function () {
      if (
        this.page == parseInt(this.page, 10) &&
        this.perPage == parseInt(this.perPage, 10)
      ) {
        this.dohvatiPodatke();
      } else {
        alert("Nisu dobri podaci!");
      }
    },
    dohvatiPodatke() {
      const api =
        "https://api.coingecko.com/api/v3/exchanges?per_page=" +
        this.perPage +
        "&page=" +
        this.page;

      this.axios.get(api).then((response) => {
        this.markets = response.data;
      });
    },
  },
};
</script>
