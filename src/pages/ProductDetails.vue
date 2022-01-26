<template>
  <section>
    <h2>{{ title }}</h2>
    <h3>${{ price }}</h3>
    <p>{{ description }}</p>
    <router-link to="/products/p2">Product č.2</router-link>
  </section>
</template>

<script>
// import { useRoute } from 'vue-router';
import { computed, inject } from 'vue';
import { useRoute } from 'vue-router';

export default {
  /////// Existujú dve varianty, kompikovanejšia a krajšia, kompikovanejšia pomocou props ktoré v main.js mam zadefinované a potom :pid je dynmické
  ////// injectnem si procucts, ktoré ma id, pid príde ako props
  ///// nakoľko je xy productov tak zmením ref na computed, aby sa vždy prekresili, ako sa zmení path

  props: ['pid'],
  setup() {
    const products = inject('products');
    // const selectedProduct = computed(() => {
    //   return products.value.find((product) => product.id === props.pid);
    // });
    const route = useRoute();
    const selectedProduct = computed(() => {
      return products.value.find((product) => product.id === route.params.pid);
    });
    const title = computed(() => {
      return selectedProduct.value.title;
    });
    const price = computed(() => {
      return selectedProduct.value.price;
    });
    const description = computed(() => {
      return selectedProduct.value.description;
    });

    return { title, price, description, products };
  },
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
