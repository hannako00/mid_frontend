<template>
  <div>

    <b-modal id="editCarModal" title="Car Entry" ok-title="Save Car" @ok="onSubmit">
      <form action="#">
        <b-form-group
          label="Brand"
          label-for="brand"
        >
          <b-form-input id="brand" v-model="car.brand" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Model"
          label-for="model"
        >
          <b-form-input id="model" v-model="car.model" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Plate Number"
          label-for="plate_number"
        >
          <b-form-input id="plate_number" v-model="car.plate_number" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Color"
          label-for="color"
        >
          <b-form-select v-model="car.color" :options="colors"></b-form-select>
        </b-form-group>

        <b-form-group
          label="Value"
          label-for="value"
        >
          <b-form-input id="value" v-model="car.value" trim></b-form-input>
        </b-form-group>

      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    car: {}
  },
  data() {
    return {
      colors: [
        {value: 'red', text: 'Red'},
        {value: 'blue', text: 'Blue'},
        {value: 'yellow', text: 'Yellow'},
        {value: 'black', text: 'Black'},
        {value: 'grey', text: 'Grey'},
        {value: 'white', text: 'White'},
      ]
    }
  },
  methods: {
    async onSubmit() {
      this.$axios.put('/api/cars/' + this.car.id, this.car)
      .then((res)=>{
        if(res.status==202) {
          alert('Update successful!')
        }
      })
      .catch((err)=>{
        alert(err.message)
      })
    }
  }
}
</script>
