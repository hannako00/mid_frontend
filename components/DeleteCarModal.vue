<template>
  <div>

    <b-modal id="deleteCarModal" title="Car Entry" ok-title="Delete Car" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this car? <br>
      {{ car.brand }} {{ car.model }}
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    car: {}
  },
  methods: {
    async onDelete() {
      this.$axios.delete('/api/cars/' + this.car.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Car is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>
