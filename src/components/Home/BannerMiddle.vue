<template>
  <v-col>
    <button class="ec" @click="calender">
      <v-card>
      <v-img
        dark
        height="450"
        width="1740"
        gradient="to bottom, rgba(0,0,0,.4), rgba(0,0,0,.4)"
        src="/img/products/astronomical.png"
      >
        <v-row align="center" class="pt-16" justify="center">
          <v-col class="text-center" cols="12">
            <h2 class="text-h3 font-weight-bold mb-4"><button class="event-calender">EVENT CALENDAR</button></h2>
            <h2 class="text-h4 subheading">
              Never miss an astronomical event again!
            </h2>
          </v-col>
        </v-row>
      </v-img>
    </v-card>
    </button>
</v-col>
</template>

<script>
export default {
  calender(){
    this.$router.push({name: 'CalenderView',});
  },
  name: "BannerMiddleComponent",
};
</script>

<style>
</style>