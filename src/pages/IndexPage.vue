<template>
  <q-page class="flex flex-center">
    <div class="row justify-center q-gutter-sm">
      <q-intersection
        v-for="product in arrayProducts"
        :key="product.id"
        once
        transition="scale"
        class="example-item"
      >
        <q-card flat bordered class="q-ma-sm">
          <img :src="product.thumbnail" />

          <q-card-section>
            <div class="text-h6">{{ product.title }}</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>
        </q-card>
      </q-intersection>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { api } from "src/boot/axios";

export default defineComponent({
  name: "IndexPage",
  setup() {
    let arrayProducts = ref([]);
    api.get("/products?limit=20").then(({ data: { products } }) => {
      console.log("products", products);
      arrayProducts.value = products;
    });

    return {
      arrayProducts,
    };
  },
});
</script>

<style lang="sass" scoped>
.example-item
  height: 290px
  width: 290px
</style>
