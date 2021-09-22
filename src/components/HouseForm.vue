<template>
  <form @submit.prevent="handleSubmit">
    <div class="form-group">
      <label for="description" class="">Description:</label>
      <input v-model="editable.description"
             type="text"
             class="form-control"
             name="description"
             id="description"
             required
      >
    </div>
    <div class="form-group">
      <label for="bedrooms" class="">Bedrooms:</label>
      <input v-model="editable.bedrooms"
             type="number"
             class="form-control"
             name="bedrooms"
             id="bedrooms"
             min="0"
             max="9999999"
             required
      >
    </div>
    <div class="form-group">
      <label for="bathsrooms" class="">Bathrooms:</label>
      <input v-model="editable.bathrooms"
             type="number"
             class="form-control"
             name="bathrooms"
             id="bathrooms"
             min="0"
             max="9999999"
             required
      >
    </div>
    <div class="form-group">
      <label for="floors" class="">Levels:</label>
      <input v-model="editable.levels"
             type="number"
             class="form-control"
             name="levels"
             id="levels"
             min="0"
             max="9999999"
             required
      >
    </div>
    <div class="form-group">
      <label for="price" class="">Price:</label>
      <input v-model="editable.price"
             type="number"
             class="form-control"
             name="price"
             id="price"
             min="0"
             max="9999999"
      >
    </div>
    <div class="form-group">
      <label for="year" class="">year:</label>
      <input v-model="editable.year"
             type="year"
             class="form-control"
             name="year"
             id="year"
      >
    </div>
    <div class="form-group">
      <label for="imgUrl" class="">imgUrl:</label>
      <input v-model="editable.imgUrl"
             type="url"
             class="form-control"
             name="imgUrl"
             id="imgUrl"
             required
      >
    </div>
    <div class="d-flex justify-content-between my-3">
      <button type="button" data-bs-dismiss="modal" aria-label="Close" class="btn text-dark lighten-20 text-uppercase selectable">
        cancel
      </button>
      <button type="submit" class="btn btn-primary text-uppercase selectable">
        submit
      </button>
    </div>
  </form>
</template>

<script>
import { ref } from '@vue/reactivity'
import { House } from '../models/House'
import { watchEffect } from '@vue/runtime-core'
import { housesService } from '../services/HousesService'
import Pop from '../utils/Pop'
export default {
  props: {
    house: { type: House, default: () => new House() }
  },
  setup(props) {
    const editable = ref({})

    watchEffect(() => {
      editable.value = { ...props.house }
    })

    return {
      editable,
      async handleSubmit() {
        try {
          if (editable.value.id) {
            await housesService.editHouse(editable.value)
          } else {
            await housesService.createHouse(editable.value)
          }
          editable.value = {}
        } catch (error) {
          Pop.toast(error.message, 'error')
        }
      }
    }
  }
}
</script>

<style>

</style>
