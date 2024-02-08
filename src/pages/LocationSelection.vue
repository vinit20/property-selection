<template>
  <div class="form-container">
    <Form :stateData="stateData" @selectedLocationData="selectLocationData" @modalOpen="modalOpen" />
    <modal :isOpen="isModalOpen" @close="closeModal" :selectedLocation="selectedLocation">
      <property-selection :selectedLocation="selectedLocation" />
    </modal>
  </div>
</template>

<script>
import Modal from "../components/Modal.vue";
import PropertySelection from "../components/PropertySelection.vue";
import Form from "../components/form.vue";
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
      stateData: [
        {
          name: "New Delhi",
          properties: [
            "delhi-property-1",
            "delhi-property-2",
            "delhi-property-3"
          ]
        },
        {
          name: "Banglore",
          properties: [
            "banglore-property-1",
            "banglore-property-2",
            "banglore-property-3"
          ]
        },
        {
          name: "Pune",
          properties: ["pune-property-1", "pune-property-2", "pune-property-3"]
        }
      ]
    };
  },
  methods: {
    selectLocationData(value) {
      this.selectedLocation = value;
    },
    modalOpen(value) {
      console.log(value, "value");
      this.isModalOpen = value;
    },
    closeModal() {
      this.isModalOpen = false;
    }
  }
};
</script>
<style scoped>
.form-container {
  width: 30%;
  background-color: #fff;
  padding: 60px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  font-size: 20px;
}
@media (max-width: 767px) {
  .form-container{
    width: 60%;
  }
}
</style>