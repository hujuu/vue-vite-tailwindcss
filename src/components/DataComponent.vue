<template>
    <div>
      <div v-if="error">{{ error }}</div>
      <div v-else-if="data">
        <p>Base: {{ data.base }}</p>
        <p>Date: {{ data.date }}</p>
        <div v-for="(rate, currency) in data.rates" :key="currency">
          {{ currency }}: {{ rate }}
        </div>
      </div>
      <div v-else>Loading...</div>
    </div>
</template>
  
<script lang="ts">
import { defineComponent, ref } from 'vue'
import axios from 'axios'
  
export default defineComponent({
    name: 'DataComponent',
    setup() {
      const data = ref(null)
      const error = ref(null)
      const url = `http://api.exchangeratesapi.io/v1/latest?access_key=`
  
      axios.get(url)
        .then(response => {
          data.value = response.data
        })
        .catch(err => {
          error.value = 'Error loading data: ' + err
        })
  
      return { data, error }
    }
})
</script>
