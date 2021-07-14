<template>

  <div>
    <NavBar />
    <EditCarModal :car="selectedCar" />
    <DeleteCarModal :car="selectedCar" @onDeleted="getAll" />
    <div class="container">
      <h1>
        Cars
        <carEntryModal class="float-right" @onAdd="getAll" />
      </h1>
      <table class="table table-bordered tabled-striped">
        <thead>
          <tr class="bg-secondary text-white">
            <th>Brand</th>
            <th>Model</th>
            <th>Plate Number</th>
            <th>Color</th>
            <th>Value</th>
            <th>&nbsp;</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="car in cars" :key="car.id">
            <td>{{car.brand}}</td>
            <td>{{car.model}}</td>
            <td>{{car.plate_number}}</td>
            <td>{{car.color}}</td>
            <td>{{car.value}}</td>
            <td>
              <b-button @click="onEdit(car)" variant="info" size="sm">
                Edit
              </b-button>
              <b-button @click="onDelete(car)" variant="danger" size="sm">
                Delete
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>

</template>

<script>
export default {
  data() {
    return {
      cars: [],
      selectedCar: {}
    }
  },
  methods: {
    async getAll() {
      await this.$axios.get('/api/cars')
      .then((res)=>{
        if(res.status==200){
          this.cars = res.data
        }
      })
    },
    onEdit(selectedCar) {
      this.selectedCar = selectedCar
      this.$bvModal.show('editCarModal')
    },
    onDelete(selectedCar) {
      this.selectedCar = selectedCar
      this.$bvModal.show('deleteCarModal')
    }
  },
  created() {
    this.getAll()
  }
}

</script>

<style>

</style>
