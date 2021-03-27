<template>
  <div class="">
    <h2 class="text-3xl my-4 py-4">List of Products</h2>
    <button
      @click="createProduct"
      class="p-2 m-2 text-center border-green-600 border border-solid rounded hover:bg-green-600 hover:text-white"
    >
      Create Product
    </button>
    <div v-if="create">
      <create-product
        @resetProduct="handleReset"
        @changedProducts="handleChanged"
      />
    </div>
    <div
      class="flex flex-row justify-around items-center space-x-4 font-bold text-lg underline"
    >
      <span class="w-1/6">ID</span>
      <span class="w-2/6">Name</span>
      <span class="w-1/6">Price</span>
      <span class="w-2/6">Actions</span>
    </div>
    <div v-if="!productsEmpty" class="my-4 space-y-4">
      <the-product
        v-for="product in products"
        :key="product.id"
        :product="product"
        @changedProducts="handleChanged"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
import utils from "@/utils";
import { Product } from "@/types";
import TheProduct from "@/components/TheProduct.vue";
import CreateProduct from "@/components/CreateProduct.vue";

const API: string = utils.API;

export default defineComponent({
  name: "ListProducts",
  components: {
    TheProduct,
    CreateProduct,
  },
  data() {
    return {
      products: [] as Product[],
      create: false,
    };
  },
  computed: {
    productsEmpty(): Boolean {
      return !(this.products.length > 0);
    },
  },
  methods: {
    fetchProducts() {
      axios
        .get(`${API}/products`)
        .then((resp) => {
          this.products = resp.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    createProduct() {
      this.create = !this.create;
    },
    handleReset() {
      this.create = false;
    },
    handleChanged() {
      this.handleReset();
      this.fetchProducts();
    },
  },

  mounted() {
    this.fetchProducts();
  },
});
</script>
