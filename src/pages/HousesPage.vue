<template>
  <div class="container-fluid px-0">
    <div class="row py-2 bg-dark mb-4 top-bar">
      <div class="col text-end">
        <button class="btn text-success lighten-30 selectable" data-bs-toggle="modal" data-bs-target="#house-form">
          Add a Listing
        </button>
      </div>
    </div>
    <div class="row ps-4">
      <House v-for="house in houses" :key="house.id" :house="house" class="col-md-3 d-flex " />
    </div>
    <Modal id="house-form">
      <template #modal-title>
        add your 🏠
      </template>
      <template #modal-body>
        <HouseForm />
      </template>
    </Modal>
  </div>
</template>

<script>
import { computed, onMounted } from '@vue/runtime-core'
import { AppState } from '../AppState'
import { housesService } from '../services/HousesService'
export default {
  setup() {
    onMounted(() => {
      housesService.getHouses()
    })

    return {
      houses: computed(() => AppState.houses)
    }
  }
}
</script>

<style>

</style>
