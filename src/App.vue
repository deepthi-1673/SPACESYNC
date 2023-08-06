<template>
  <v-app app>
    <v-app-bar color="dark" dark app>
      <img src="/img/products/logo-removebg-preview.png" alt="" style="height: auto; size: 10cm; width: 15vw;">
      <v-spacer></v-spacer>
      
      <v-app-bar-nav-icon
        @click.stop="drawer = !drawer"
        v-if="$vuetify.breakpoint.mobile"
      ></v-app-bar-nav-icon>
      
      <template v-if="!$vuetify.breakpoint.mobile">
        <v-btn elevation="0" class="mr-3" to="/"> Home </v-btn>
        <v-btn elevation="0" class="mr-3" to="/products"> Agencies </v-btn>
        <v-btn elevation="0" class="mr-3" to="/travels"> Calendar </v-btn>
        <!-- <v-btn elevation="0" class="mr-3" to="/configurator"> Cargo<small>Bêta</small> </v-btn> -->
        <v-btn
          v-if="!publicKey"
          outlined
          elevation="0"
          class="mr-3"
          color="primary"
          to="/register"
        >
          Connect wallet
        </v-btn>
        <v-btn
          v-if="publicKey"
          outlined
          elevation="0"
          class="mr-3"
          color="primary"
          to="/dashboard"
        >
          Dashboard
        </v-btn>
        <!-- <v-btn elevation="0" class="mr-3" color="primary" to="/cart">
          Cart
        </v-btn> -->
      </template>
      <v-chip v-if="publicKey" color="success">
        <i class="cf mr-3 cf-xlm"></i>
        <span class="font-weight-bold">{{
          walletBalance
            ? new Intl.NumberFormat("de-DE", {
                style: "currency",
                currency: "XLM",
              }).format(walletBalance)
            : "--.--"
        }}</span>
      </v-chip>

      <v-navigation-drawer
        v-model="drawer"
        v-if="$vuetify.breakpoint.mobile"
        absolute
        app
      >
        <v-col>
          <h1>SPACESYNC</h1>
        </v-col>
        <v-list nav dense>
          <v-list-item to="/">
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>

          <v-list-item to="/products">
            <v-list-item-title>Agencies</v-list-item-title>
          </v-list-item>

          <v-list-item to="/travels">
            <v-list-item-title>Calendar</v-list-item-title>
          </v-list-item>

          <v-list-item to="/configurator">
            <v-list-item-title>Cargo<small>Bêta</small></v-list-item-title>
          </v-list-item>
        </v-list>
        <v-col>
          <v-btn
            v-if="publicKey"
            outlined
            block
            elevation="0"
            color="primary"
            to="/dashboard"
          >
            Dashboard
          </v-btn>

          <!-- <v-btn elevation="0" class="my-2" color="primary" to="/cart" block>
            Cart
          </v-btn> -->
          <v-btn
            v-if="!publicKey"
            outlined
            elevation="0"
            color="primary"
            to="/register"
          >
            Connect wallet
          </v-btn>
        </v-col>
      </v-navigation-drawer>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
    <v-footer>
      <v-container>
        <v-row class="py-0">
          <v-col>
            <!-- <router-link tag="a" to="/" style="text-decoration: none; color: white;">Home</router-link><br />
            <router-link tag="a" to="/products">Agencies</router-link><br />
            <router-link tag="a" to="/travels">Calendar</router-link><br /> -->
          </v-col>
          <v-col class="text-center">
            <!-- <router-link tag="a" to="/legal-policy">Legals</router-link><br /> -->
          </v-col>
            <div class="text-h4" style="justify-content: center;align-items: center;display: flex;position: relative;right: 37vw; margin-bottom: 25px;">SPACESYNC</div><br />
        </v-row>
        <v-col cols="12" class="text-center">
          Copyright {{ $moment().format("YYYY") }} © - SPACESYNC
        </v-col>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "App",
  computed: {
    ...mapState(["publicKey", "walletBalance"]),
  },
  data: () => ({
    drawer: false,
  }),
  methods: {
    async getBalance() {
      this.$axios
        .get(`https://horizon-testnet.stellar.org/accounts/${this.publicKey}`)
        .then((res) => {
          const { data } = res;
          let xlmBalance = data.balances.find(
            (map) => map.asset_type == "native"
          );
          this.$store.dispatch("setWalletBalance", xlmBalance.balance);
        });
    },
  },
  mounted() {
    setInterval(() => {
      if (this.publicKey) {
        this.getBalance();
      }
    }, 5000);
  },
};
</script>

<style lang="scss">
$body-font-family: "Maven Pro";
$title-font: "Maven Pro";
.v-application {
  font-family: $body-font-family, sans-serif !important;
  .title {
    // To pin point specific classes of some components
    font-family: $title-font, sans-serif !important;
  }
}
</style>
