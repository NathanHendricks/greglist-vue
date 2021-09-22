<template>
  <div class="mb-4 listing card p-0 justify-content-center text-center">
    <router-link :to="{name: 'House', params: { houseId: house.id }}">
      <img :src="house.img" alt="listing image" class="rounded img-fluid">
      <div class="card-body">
        <h5 class="d-flex justify-content-between">
          <span>Bedrooms: {{ house.bedrooms }} - Bathrooms: {{ house.bathrooms }}</span>
          <span>$ {{ house.price }} </span>
        </h5>
        <p> Year: {{ house.year }} Description: {{ house.description }}</p>
      </div>
    </router-link>
  </div>
</template>

<script>
import { House } from '../models/House'
import { logger } from '../utils/Logger'
export default {
  props: {
    house: { type: House, required: true }
  },
  setup() {
    return {
      deleteHouse() {
        logger.log('working?')
      }
    }
  }
}
</script>

<style>

</style>
