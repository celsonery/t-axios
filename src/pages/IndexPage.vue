<template>
  <q-page class="flex flex-center">
    <q-card>
      <q-card-section>
        {{ responseData }}
      </q-card-section>

      <q-separator/>

      <q-card-actions vertical>
        <q-btn @click.prevent.stop="getProducts">Produtos</q-btn>
        <q-btn @click.prevent.stop="getCompra">Comprar APP</q-btn>
      </q-card-actions>
    </q-card>
    teste
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
    },

    getProducts () {
      window.inAppPurchases.getAllProductInfo(['br.com.bagarote.teste_celso.produto1'])
        .then((response) => {
          console.log('Success: ' + response)
          alert('Success: ' + JSON.stringify(response))
        })
        .catch((err) => {
          console.log('Err: ' + err)
          alert('Err: ' + JSON.stringify(err))
        })
    },

    getCompra () {
      window.inAppPurchases.purchase('br.com.bagarote.teste_celso.produto1')
        .then((response) => {
          console.log('Success: ' + response)
          alert('Success: ' + JSON.stringify(response))
        })
        .catch((err) => {
          console.log('Err: ' + err)
          alert('Err: ' + JSON.stringify(err))
        })
    }

  },

  mounted () {
    this.getData()
  }
})
</script>
