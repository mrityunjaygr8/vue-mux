<template>
  <div class="my-4 px-2 py-2 border border-gray-600 bg-white">
    <p class="text-xl font-semibold">Create Product</p>

    <form @submit.prevent class="grid grid-cols-2 grid-rows-2 justify-center">
      <input
        type="text"
        v-model="product.name"
        placeholder="Product Name"
        class="p-2 m-2 bg-gray-50 border border-solid border-gray-600"
      />
      <input
        type="text"
        v-model.number="product.price"
        placeholder="Product Price"
        class="p-2 m-2 bg-gray-50 border border-solid border-gray-600"
      />
      <input
        type="submit"
        value="Create"
        @click="createProduct"
        class="m-2 p-2 bg-gray-50 border border-solid border-green-600 hover:bg-green-600 hover:text-white cursor-pointer"
      />
      <input
        type="reset"
        value="Reset"
        @click="reset"
        class="m-2 p-2 bg-gray-50 border border-solid border-red-600 hover:bg-red-600 hover:text-white cursor-pointer"
      />
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Product } from "@/types";
import axios from "axios";
import utils from "@/utils";

const API: string = utils.API;

export default defineComponent({
  name: "CreateProduct",
  data() {
    return {
      product: {} as Product,
    };
  },
  methods: {
    reset() {
      this.product = {} as Product;
      this.$emit("resetProduct");
    },
    createProduct() {
      axios
        .post(`${API}/product`, this.product)
        .then(() => {
          this.$emit("changedProducts");
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
});
</script>
