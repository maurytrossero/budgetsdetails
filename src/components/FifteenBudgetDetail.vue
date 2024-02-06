<template>
  <div class="presupuesto-container">
    
    <div class="logo-container">
      <img src="https://scontent.fcor3-1.fna.fbcdn.net/v/t39.30808-6/326524611_1565285560665566_1754105422097280677_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=efb6e6&_nc_ohc=wePk7zgEIvkAX-WLH9L&_nc_ht=scontent.fcor3-1.fna&cb_e2o_trans=q&oh=00_AfBl6DQYV-eNFhNTzONvKfO6tB7QZEVCLJ3PUg5OHjI31w&oe=65C63DDB" alt="Logo" class="logo-image" />
    </div>

    <h1 class="titulo">Calculador de Presupuestos</h1>

    <!-- Sección de Precio Base -->
    <div class="seccion-precio">
      <label>Precio por 2 horas de cobertura </label>
      <input v-model="precioBase" type="number" />
    </div>

    <!-- Sección de Valor Hora Extra -->
    <div class="seccion-hora-extra">
      <label>Precio por hora extra </label>
      <input v-model="costoHoraExtra" type="number" />
    </div>

    <!-- Sección de Meses de Proyección -->
    <div class="seccion-meses-proyeccion">
      <label>Cantidad de meses para el evento </label>
      <input v-model="mesesProyectados" type="number" />
    </div>

    <!-- Sección de Inflación Anual -->
    <div class="seccion-inflacion-anual">
      <label>Inflación interanual %</label>
      <input v-model="inflacionAnual" type="number" /> 
    </div>

    <!-- Sección de Items -->
    <div class="seccion-items">
      <label class="subtitulo">Selecciona los Items</label>
      <div v-for="item in items" :key="item.value" class="item-container">
        <input
          type="checkbox"
          :id="item.value"
          :value="item.value"
          v-model="selectedItems"
        />
        <label :for="item.value" class="item-label">{{ item.label }}</label>
        <input
          type="number"
          :id="item.value + 'Horas'"
          v-model="item.horasTrabajadas"
          :disabled="!selectedItems.includes(item.value)"
          class="horas-input"
        />
        <label :for="item.value + 'Horas'" class="item-label">Horas Trabajadas</label>
        <p v-if="selectedItems.includes(item.value)" class="costo-text">
          Costo {{ item.label }}: $ {{ calcularCostoItem(item) }}
        </p>
      </div>
    </div>

    <!-- Resultados -->
    <div class="resultados">
      <h2 class="subtitulo">Resultado del Presupuesto</h2>
      <p class="total-presupuesto">Total Presupuesto: $ {{ mostrarPresupuesto }}</p>
      <p class="precio-financiado">Precio Financiado: $ {{ mostrarPrecioFinanciado }}</p>
    </div>
  </div>
</template>


<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      precioBase: 50000,
      costoHoraExtra: 14000,
      mesesProyectados: 1,
      inflacionAnual: 220,
      selectedItems: [] as string[],
      items: [
        { label: 'Fiesta', value: 'fiesta', horasTrabajadas: 9 },
        { label: 'Sesion de fotos / Book', value: 'segundoItem', horasTrabajadas: 2 },
        { label: 'Pintada de calle/ Pancarta', value: 'tercerItem', horasTrabajadas: 2 },
      ] as { label: string; value: string; horasTrabajadas: number }[],
    };
  },

  methods: {
    calcularPresupuestoTotal(): number {
      return this.items
        .filter(item => this.selectedItems.includes(item.value))
        .reduce((total, item) => total + this.calcularCostoItem(item), 0);
    },
    calcularCostoItem(item: { label: string; value: string; horasTrabajadas: number }): number {
      const costoBase = this.calcularCostoBase(item.horasTrabajadas);
      return costoBase * this.calcularInflacionProyectada();
    },
    calcularCostoBase(horasTrabajadas: number): number {
      if (horasTrabajadas === 2) {
        return this.precioBase;
      } else if (horasTrabajadas > 2) {
        return this.precioBase + ((horasTrabajadas - 2) * this.costoHoraExtra);
      } else if (horasTrabajadas === 1) {
        return this.precioBase / 2;
      } else {
        return 0;
      }
    },
    calcularInflacionProyectada(): number {
      // Tu lógica de cálculo de inflación proyectada aquí
      return 1;
    },
    calcularPresupuesto(): number {
      return this.items
        .filter(item => this.selectedItems.includes(item.value))
        .reduce((total, item) => total + this.calcularCostoItem(item), 0);
    },
    calcularPrecioFinanciado(): string {
      const presupuesto = this.calcularPresupuesto();
      const inflacionMensual = this.inflacionAnual / 12 / 100;
      const resultado = presupuesto + presupuesto * this.mesesProyectados * inflacionMensual;

      if (resultado && typeof resultado === 'number') {
        return resultado.toFixed(2);
      } else {
        return '0.00';
      }
    },
  },

  computed: {
    mostrarPresupuesto(): string {
      const presupuesto = this.calcularPresupuesto();
      return presupuesto && typeof presupuesto === 'number' ? presupuesto.toFixed(2) : '0.00';
    },
    mostrarPrecioFinanciado(): string {
      const precioFinanciado = this.calcularPrecioFinanciado();
      return precioFinanciado && typeof precioFinanciado === 'string' ? precioFinanciado : '0.00';
    },
  },
});
</script>



<style scoped>
/* Estilos Generales */
.presupuesto-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 10px;
  font-family: 'Arial', sans-serif;
  background-color: #f5f5f5;
}

/* Contenedor de la imagen */
/* Contenedor de la imagen */
.logo-container {
  width: 100px; /* Ajusta el tamaño del contenedor según tus necesidades */
  height: 100px; /* Ajusta el tamaño del contenedor según tus necesidades */
  background-color: white; /* Fondo blanco */
  border-radius: 50%; /* Esquinas redondeadas */
  overflow: hidden; /* Asegura que la imagen no sobresalga del contenedor redondeado */
  margin: 0 auto; /* Centra el contenedor horizontalmente */
}

.logo-image {
  width: 100%; /* Ajusta el ancho de la imagen según tus necesidades */
  height: auto;
  display: block;
}

.titulo {
  font-size: 20px;
  margin-bottom: 15px;
  color: #333;
}

/* Secciones */
.seccion-precio,
.seccion-hora-extra,
.seccion-meses-proyeccion,
.seccion-inflacion-anual,
.seccion-items,
.resultados {
  background-color: #fff;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 15px;
}

.subtitulo {
  font-size: 16px;
  margin-bottom: 10px;
  color: #555;
}

/* Elementos de Item */
.item-container {
  flex-direction: column;
  margin-bottom: 10px;
}

.item-label,
.horas-input,
.costo-text {
  width: 100%;
  margin-right: 0;
}

.horas-input {
  width: 60px;
  margin-right: 10px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.costo-text {
  font-size: 12px;
  color: #777;
  margin-top: 5px;
}

/* Resultados */
.total-presupuesto,
.precio-financiado {
  font-size: 16px;
  margin-bottom: 10px;
  color: #333;
}

/* Estilos para Inputs específicos */
.seccion-precio input,
.seccion-hora-extra input,
.seccion-meses-proyeccion input,
.seccion-inflacion-anual input {
  width: 100%;
  padding: 10px; /* Ajusta el padding según tus preferencias */
  margin-bottom: 10px; /* Espaciado inferior */
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 14px; /* Ajusta el tamaño de fuente según tus preferencias */
}

/* Ajustes para Dispositivos Móviles */
@media screen and (max-width: 600px) {
  .seccion-precio input,
  .seccion-hora-extra input,
  .seccion-meses-proyeccion input,
  .seccion-inflacion-anual input {
    margin-bottom: 15px; /* Añade más espacio inferior en dispositivos móviles */
  }
}
</style>
