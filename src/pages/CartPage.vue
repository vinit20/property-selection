<template>
  <div class="cart-page-main">
    <h2>Cart Page</h2>
    <div class="selected-data">
      <span>
        <b>Selected Location:</b>
        {{ this.$route.query.selectedLocation }}
      </span>
      <span>
        <b>Selected Properties:</b>
        {{ Array.isArray($route.query.selectedProperty) ? $route.query.selectedProperty.join(', ') : $route.query.selectedProperty }}
      </span>
    </div>
    <Form @formSubmission="formSubmit"/>
    <p class="submit-form" v-if="formSubmitSuccessfully">Form Submitted Successfully</p>
  </div>
</template>

<script>
import Form from "../components/form.vue";
export default {
  name: "cart-page",
  data(){
    return {
      formSubmitSuccessfully: false
    }
  },
  components: {
    Form
  },
  methods: {
    formSubmit(value){
      this.formSubmitSuccessfully = value
      setTimeout(() => {
        this.formSubmitSuccessfully = false
      }, 5000);
    }
  }
};
</script>

<style scoped>
.cart-page-main {
  width: 30%;
  background-color: #fff;
  padding: 60px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  font-size: 20px;
}
h2{
  text-align: center;
  margin-bottom: 60px;
}
.selected-data {
  display: flex;
  flex-direction: column;
}
.selected-data span {
  margin-bottom: 10px;
}
.submit-form{
  color: green;
}

@media (max-width: 600px) {
 .cart-page-main{
  width: auto;
  padding: 60px;
 }
}
</style>