<template>
  <form>
    <div class="form-group" v-if="$route.name != 'Cart'">
      <label for="location">Select Location:</label>
      <select v-model="selectedLocation" id="location" name="location" class="select-dropdown">
        <option
          class="option"
          v-for="state in stateData"
          :key="state.id"
          :value="state.name"
        >{{ state.name }}</option>
      </select>
    </div>
    <div class="form-group-mt" v-if="$route.name === 'Cart'">
      <div class="form-group">
        <label for="name">Name:</label>
        <input type="text" v-model="userData.name" id="name" name="name" class="input-field" />
      </div>
      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" v-model="userData.email" id="email" name="email" class="input-field" />
      </div>
      <div class="form-group">
        <label for="phone">Phone:</label>
        <input type="tel" v-model="userData.phone" id="phone" name="phone" class="input-field" />
      </div>
    </div>
    <button v-if="$route.name != 'Cart'" @click.prevent="submitForm" class="btn">Submit</button>
    <button :class="{active: userData.name=='' || userData.email=='' || userData.phone==''}" :disabled="userData.name=='' || userData.email=='' || userData.phone==''" v-if="$route.name === 'Cart'" @click.prevent="submitFormWithUserData" class="btn">Submit</button>
  </form>
</template>

<script>
export default {
  name: "form-page",
  props: {
    stateData: Array
  },
  data() {
    return {
      selectedLocation: "New Delhi",
      modalOpen: false,
      userData: {
        name: "",
        email: "",
        phone: ""
      },
      formSubmit: false
    };
  },
  methods: {
    submitForm() {
      this.selectedLocationData = this.stateData.filter(state => {
        return this.selectedLocation == state.name;
      });
      this.modalOpen = true;
      this.$emit("selectedLocationData", this.selectedLocationData);
      this.$emit("modalOpen", this.modalOpen);
    },
    submitFormWithUserData() {
        this.userData = {}
        this.formSubmit = true;
        this.$emit('formSubmission', this.formSubmit)
    }
  }
};
</script>

<style scoped>
input {
  width: 100%;
  padding: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  background-color: #fff;
  box-sizing: border-box;
}

.form-group {
  margin-bottom: 20px;
}
.form-group-mt{
    margin-top: 16px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.select-dropdown {
  width: 100%;
  padding: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  background-color: #fff; /* Set background color */
}

.select-dropdown:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}
.option {
  padding: 16px !important;
}

.btn {
  display: block;
  width: 100%;
  padding: 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
}

.btn:hover {
  background-color: #0056b3;
}
.btn{
  margin-top: 20px;
}
.active{
  cursor: not-allowed;
}
</style>