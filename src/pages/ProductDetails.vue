<template>
  <section>
    <h2>{{ title }}</h2>
    <h3>${{ price }}</h3>
    <p>{{ description }}</p>
    <router-link :to="`/products/${pid == 'p1' ? 'p2' : 'p1'}`"
      >Product {{ pid == 'p1' ? 2 : 1 }}</router-link
    >
  </section>
</template>

<script>
import { inject, computed } from 'vue';

export default {
  props: ['pid'],
  setup(props) {
    console.log('productDetails', props.pid);
    const products = inject('products');

    // const title = ref('');
    // const price = ref(null);
    // const description = ref('');

    const selectedProduct = computed(() =>
      products.value.find(prd => prd.id === props.pid)
    );
    // console.log('selectedProduct', selectedProduct.value);
    const title = computed(() => selectedProduct.value.title);
    const price = computed(() => selectedProduct.value.price);
    const description = computed(() => selectedProduct.value.description);

    return { title, price, description };
  }
};
</script>

<style scoped>
section {
  margin: 3rem auto;
  max-width: 40rem;
  padding: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
}
</style>
