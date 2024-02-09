<template>
  <div class="form-container">
    <h2>OMKATECH ASSIGNMENT</h2>
    <Form :stateData="stateData" @selectedLocationData="selectLocationData" @modalOpen="modalOpen" />
    <!-- display the property selection component inside modal by using slot there -->
    <modal :isOpen="isModalOpen" @close="closeModal" :selectedLocation="selectedLocation">
      <property-selection :selectedLocation="selectedLocation" />
    </modal>
  </div>
</template>

<script>
import Modal from "../components/Modal.vue";
import PropertySelection from "../components/PropertySelection.vue";
import Form from "../components/FormPage.vue";
import STATE_DATA from "../utils/state-data.json";
export default {
  name: "location-selection",
  components: {
    PropertySelection,
    Form,
    Modal
  },
  data() {
    return {
      selectedLocation: [],
      isModalOpen: false,
      stateData: STATE_DATA
    };
  },
  methods: {
    //location selection
    selectLocationData(value) {
      this.selectedLocation = value;
    },
    //open modal
    modalOpen(value) {
      console.log(value, "value");
      this.isModalOpen = value;
    },
    // close modal
    closeModal() {
      this.isModalOpen = false;
    }
  }
};
</script>

<style lang="less" scoped>
// use less css preprocessor
.form-container {
  width: 30%;
  background-color: #fff;
  padding: 30px 60px 60px 60px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  h2 {
    text-align: center;
    margin-bottom: 50px;
  }
}
@media (max-width: 767px) {
  .form-container {
    width: 100%;
    margin: 20px;
    padding: 20px;
  }
}
</style>