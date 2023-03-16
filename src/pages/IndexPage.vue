<template>
  <q-page class="flex flex-center">
    <q-card>
      <q-card-section>
        {{ responseData }}
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'IndexPage',

  data: () => {
    return {
      responseData: ''
    }
  },

  methods: {
    async getData () {
      await axios.get('https://api-dev.eurekaplus.com.br/api/comecarJogo/4')
        .then((response) => {
          console.log(response)
          this.responseData = response.data
        })
        .catch((err) => {
          console.log(err)
          this.responseData = err.getMessage()
        })
    }
  },

  mounted () {
    this.getData()
  }
})
</script>
