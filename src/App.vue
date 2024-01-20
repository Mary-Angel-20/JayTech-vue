/**Diseno */
<template>
  <Header
    :carrito="carrito"
    :producto="producto"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @agregar-carrito="agregarCarrito"
    @eliminar-producto="eliminarProducto"
    @vaciar-carrito="vaciarCarrito"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Our Collection</h2>
    <div class="row mt-5">
      <Productos
        v-for="producto in productos"
        :key="producto"
        :producto="producto"
        @agregar-carrito="agregarCarrito"
      />
    </div>
  </main>

  <Footer />
</template>

/**Codigo */
<script setup>
import { ref, reactive, onMounted, watch} from "vue";
import { db } from "./data/productos";
import Header from "./components/header.vue";
import Footer from "./components/footer.vue";
import Productos from "./components/Productos.vue";

const productos = ref([]);
const carrito = ref([]);
const producto = ref({});

watch(carrito, ()=>{
guardarLocalStorage ()
},{
  deep:true
})

onMounted(() => {
  productos.value = db;
  producto.value = db[3];

  const carritoStorage= localStorage.getItem('carrito')
  if(carritoStorage){
    carrito.value=JSON.parse(carritoStorage)
  }
});
const guardarLocalStorage =() =>{

  localStorage.setItem('carrito', JSON.stringify(carrito.value))
}


const agregarCarrito = (producto) => {
  const existeCarrito = carrito.value.findIndex(
    (product) => product.id === producto.id
  );
  if (existeCarrito >= 0) {
    carrito.value[existeCarrito].cantidad++;
  } else {
    producto.cantidad = 1;
    carrito.value.push(producto);
  }
};

const decrementarCantidad = (id) => {
  const index = carrito.value.findIndex((product) => product.id === id);
  if (carrito.value[index].cantidad <= 1) return;
  carrito.value[index].cantidad--;
};

const incrementarCantidad = (id) => {
  const index = carrito.value.findIndex((product) => product.id === id);
  carrito.value[index].cantidad++;
};

const eliminarProducto =(id) => {
  carrito.value=carrito.value.filter(product=>product.id !==id)
};

const vaciarCarrito =() => {
  carrito.value=[]

};
</script>

