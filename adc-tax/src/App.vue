<template>
  <h1>Withholding TAX</h1>
<TaxForm/>

</template>
<script>
import TaxForm from './components/TaxForm.vue';

export default {
  name: 'App',
  components: {
    TaxForm
  }
}
</script>

<style>
h1{
  padding-left: 5% ;
  font-weight: bold;
  text-decoration: underline;
  text-decoration-thickness: 6px;
  text-decoration-color: #6f399b;
  text-underline-offset: 8px;
  
}
</style>
