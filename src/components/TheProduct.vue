<template>
  <div class="md:container">
    <div class="flex flex-row justify-around items-center space-x-4">
      <span class="w-1/6">{{ product.id }}</span>
      <span class="w-2/6">{{ product.name }}</span>
      <span class="w-1/6">{{ product.price }}</span>

      <div class="w-2/6 flex">
        <button
          @click="editToggle"
          class="m-1 p-1 bg-transparent border border-solid border-green-600 hover:bg-green-600 hover:text-white cursor-pointer rounded w-1/2"
        >
          Edit
        </button>
        <button
          @click="deleteProduct"
          class="m-1 p-1 bg-transparent border border-solid border-red-600 hover:bg-red-600 hover:text-white cursor-pointer rounded w-1/2"
        >
          Delete
        </button>
      </div>
    </div>

    <edit-product
      v-if="edit"
      :product="product"
      @resetProduct="handleReset"
      @editProduct="handleEdit"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Product } from "@/types";
import utils from "@/utils";
import axios from "axios";
import EditProduct from "@/components/EditProduct.vue";

const API: string = utils.API;

export default defineComponent({
  name: "TheProduct",
  components: {
    EditProduct,
  },
  props: {
    product: {
      type: Object as PropType<Product>,
      required: true,
    },
  },
  data() {
    return {
      edit: false,
    };
  },
  methods: {
    deleteProduct() {
      axios
        .delete(`${API}/product/${this.product.id}`)
        .then(() => {
          this.$emit("changedProducts");
        })
        .catch((err) => {
          console.log(err);
        });
    },
    editToggle() {
      this.edit = !this.edit;
    },
    handleReset() {
      this.edit = false;
    },
    handleEdit(payload: Product) {
      axios
        .put(`${API}/product/${this.product.id}`, payload)
        .then(() => {
          this.editToggle();
          this.$emit("changedProducts");
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
});
</script>

