<script setup>
const props = defineProps({
  producto: {
    type: Object,
    required: true,
  },
});
defineEmits(["agregar-carrito"]);
</script>

<template>
  <div class="col-md-6 col-lg-4 my-4 row align-items-center">
    <div class="col-4">
      <img
        class="img-fluid"
        :src="'/img/' + producto.imagen + '.jpg'"
        :alt="'imagen case' + producto.nombre"
      />
    </div>
    <div class="col-8">
      <h3 class="text-black fs-4 fw-bold text-uppercase">
        {{ producto.nombre }}
      </h3>
      <p>{{ producto.descripcion }}</p>
      <p class="fw-black text-primary fs-3">$ {{ producto.precio }}</p>
      <button
        type="button"
        class="btn btn-pink w-100"
        @click="$emit('agregar-carrito', producto)"
      >
        Agregar al Carrito
      </button>
    </div>
  </div>
  <!-- FIN GUITARRA -->
</template>


