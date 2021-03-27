<template>
  <div class="bg-white">
    <hr class="w-full border-t-2 border-gray-600 mt-2" />
    <form
      @submit.prevent
      class="grid grid-cols-2 grid-rows-2 justify-center px-2 border-b-2 border-gray-600"
    >
      <input
        type="text"
        v-model="newProduct.name"
        placeholder="Product Name"
        class="p-2 m-2 bg-gray-50 border border-gray-600"
      />
      <input
        type="text"
        v-model.number="newProduct.price"
        placeholder="Product Place"
        class="p-2 m-2 bg-gray-50 border border-gray-600"
      />
      <input
        type="submit"
        value="Edit"
        @click="editProduct"
        class="p-2 m-2 bg-gray-50 border border-green-600 hover:bg-green-600 hover:text-white cursor-pointer"
      />
      <input
        type="button"
        value="Reset"
        @click="reset"
        class="p-2 m-2 bg-gray-50 border border-red-600 hover:bg-red-600 hover:text-white cursor-pointer"
      />
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Product } from "@/types";

export default defineComponent({
  name: "EditProduct",
  props: {
    product: {
      type: Object as PropType<Product>,
      required: true,
    },
  },
  data() {
    return {
      newProduct: Object.assign({}, this.product) as Product,
    };
  },
  methods: {
    reset() {
      this.newProduct = Object.assign({}, this.product) as Product;
      this.$emit("resetProduct");
    },
    editProduct() {
      this.$emit("editProduct", this.newProduct);
    },
  },
});
</script>

