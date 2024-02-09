<template>
  <div class="property-selection-main">
    <!-- using the loop here for showing the properties according to the location -->
    <div class="property" v-for="state in selectedLocation" :key="state.id">
      <div v-for="(property, index) in state.properties" :key="index">
        <div class="inputs">
          <div>
            <input
              type="checkbox"
              v-model="selectProperty"
              :value="property"
            />
            <span>{{ property }}</span>
          </div>
        </div>
      </div>
      <div v-if="selectProperty.length" class="selected-property">
        Selected Properties:
        <span>
          <b>{{ selectProperty.join(', ') }}</b>
        </span>
      </div>
    </div>
    <div class="button" v-if="selectedLocation.length">
      <button
        :class="{active: !selectProperty.length}"
        :disabled="!selectProperty.length"
        @click="addToCart"
      >Add to cart</button>
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
    addToCart() {
      // this code is used to change the route from home page to cart page with query
      this.$router.push({
        path: "/cart",
        query: {
          selectedLocation: this.selectedLocation[0].name,
          selectedProperty: this.selectProperty
        }
      });
    }
  }
};
</script>

<style lang="less" scoped>
// use less css preprocessor
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
  button {
    padding: 12px 50px;
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
}
.active {
  cursor: not-allowed;
}
.selected-property {
  margin-top: 20px;
  span {
    color: #007bff;
  }
}
</style>