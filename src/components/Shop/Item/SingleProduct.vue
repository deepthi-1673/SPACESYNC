<template>
  <v-row>
    <v-col md="6" col="12">
      <v-img v-if="product.featured_image" :src="product.featured_image" />
    </v-col>
    <v-col md="6" col="12">
      <h1>{{ product.title }}</h1>
      <p class="" style="font-size: 35px;">
        {{ product.description }}
      </p>
      <h2 class="mt-5 noDecoration">
        <p style="font-size: 15px">{{ product.URI }}</p>
      </h2>
      <v-col>
        <h4 class="mt-8">Total Funding</h4>
        <h3>{{ product.price }} $</h3>
        <v-divider class="my-5" />
        
        <div>{{ product.content }}</div>
        <div class="mt-10"></div>
        <h4>Available Technologies</h4>
        <div class="mt-12"></div>
        <tbody>
          <tr>
            <td>{{ product.v1 }}</td>
          </tr>
          <!-- <v-divider class="my-7" /> -->
          <div class="mt-12"></div>
          <tr>
            <td>{{ product.v2 }}</td>
          </tr>
          <div class="mt-12"></div>
          <!-- <v-divider class="my-7" /> -->
          <tr>
            <td>{{ product.v3 }}</td>
          </tr>
          <div class="mt-12"></div>
          <!-- <v-divider class="my-7" /> -->
          <tr>
            <td>{{ product.v4 }}</td>
          </tr>
        </tbody>
      </v-col>
    </v-col>
  </v-row>
</template>

<script>
import launches from "@/assets/launches/launches-list.json";
export default {
  props: {
    product: {
      type: Object,
      default: () => ({
        title: null,
        featured_image: null,
        weight: null,
        from: {
          planet: null,
        },
        provider: {
          name: null,
        },
        category: {
          name: null,
        },
        description: null,
        price: null,
        currency: null,
      }),
    },
  },
  methods: {
    addProductToCart() {
      this.$store.dispatch("addToCart", { ...this.product, ...this.options });
    },
  },
  data: () => ({
    options: {
      arrival: null,
      launch: null,
    },
    launches: launches,
    addToCart: false,
  }),
};
</script>
