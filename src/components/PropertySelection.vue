<template>
  <div class="property-selection-main">
    <div class="property" v-for="state in selectedLocation" :key="state.id">
      <div v-for="(property, index) in state.properties" :key="index">
        <div class="inputs">
          <div>
            <input
              type="checkbox"
              @change="propertySelect"
              v-model="selectProperty"
              :value="property"
            />
            <span>{{ property }}</span>
          </div>
        </div>
      </div>
    </div>
    <div class="button" v-if="selectedLocation.length">
      <button :class="{active: !selectProperty.length}" :disabled="!selectProperty.length" @click="addToCart">Add to cart</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "property-selection",
  props: ["selectedLocation"],
  data() {
    return {
      selectProperty: []
    };
  },
  methods: {
    propertySelect() {
      console.log(this.selectProperty);
    },
    addToCart(){
        this.$router.push({ path: '/cart', query: { selectedLocation: this.selectedLocation[0].name, selectedProperty: this.selectProperty } });
    }
  }
};
</script>

<style scoped>
.inputs {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}
.inputs div {
  margin-bottom: 10px;
}
.inputs input {
  margin-right: 8px;
}
.button {
  text-align: right;
  margin-top: 20px;
}
button {
  padding: 16px 50px;
  width: 100%;
  background-color: #007bff;
  color: #fff;
  font-size: 16px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
}
.btn:hover {
  background-color: #0056b3;
}
.active{
    cursor: not-allowed;
}
</style>