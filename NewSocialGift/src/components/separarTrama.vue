<template>
  <!-- Puedes agregar aquí tu código HTML -->
</template>

<script>
export default {
  methods: {
    obtenerIdDesdeToken(token) {
      const [headerB64, payloadB64, signatureB64] = token.split('.')
      const header = JSON.parse(atob(headerB64))
      const payload = JSON.parse(atob(payloadB64))
      const { id } = payload
      return id
    }
  }
}
</script>
