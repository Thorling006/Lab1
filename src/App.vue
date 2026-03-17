<template>
  <div class="contenedor">
    <header class="encabezado">
      <h1>Sistema de Préstamo de Cubículos</h1>
      <p>Registro y control de reservas para estudiantes universitarios</p>
    </header>

    <main class="principal">
      <section class="panel">
        <h2>Registrar reserva</h2>

        <div v-if="mensaje" class="mensaje exito">
          {{ mensaje }}
        </div>

        <div v-if="error" class="mensaje error">
          {{ error }}
        </div>

        <form @submit.prevent="registrarReserva" class="formulario">
          <div class="campo">
            <label for="nombre">Nombre del estudiante</label>
            <input
              id="nombre"
              type="text"
              v-model="nombre"
              placeholder="Ejemplo: Omar Ventura"
            />
          </div>

          <div class="campo">
            <label for="carnet">Carné</label>
            <input
              id="carnet"
              type="text"
              v-model="carnet"
              placeholder="Ejemplo: SMSS000123"
            />
          </div>

          <div class="campo">
            <label for="cubiculo">Cubículo</label>
            <select id="cubiculo" v-model="cubiculo">
              <option value="">Seleccione un cubículo</option>
              <option value="Cubículo 1">Cubículo 1</option>
              <option value="Cubículo 2">Cubículo 2</option>
              <option value="Cubículo 3">Cubículo 3</option>
              <option value="Cubículo 4">Cubículo 4</option>
            </select>
          </div>

          <div class="campo">
            <label for="motivo">Motivo de uso</label>
            <textarea
              id="motivo"
              v-model="motivo"
              placeholder="Escriba el motivo de la reserva"
            ></textarea>
          </div>

          <button
            type="submit"
            class="btn-guardar"
            v-bind:disabled="nombre.trim() === '' || carnet.trim() === '' || cubiculo === '' || motivo.trim() === ''"
          >
            Guardar reserva
          </button>
        </form>
      </section>

      <section class="panel">
        <h2>Reservas registradas</h2>

        <div class="filtro">
          <input type="checkbox" id="soloActivas" v-model="soloActivas" />
          <label for="soloActivas">Mostrar solo activas</label>
        </div>

        <article
          class="tarjeta"
          v-for="reserva in reservasFiltradas"
          :key="reserva.id"
        >
          <h3>{{ reserva.nombre }}</h3>
          <p><strong>Carné:</strong> {{ reserva.carnet }}</p>
          <p><strong>Cubículo:</strong> {{ reserva.cubiculo }}</p>
          <p><strong>Motivo:</strong> {{ reserva.motivo }}</p>
          <p>
            <strong>Estado:</strong>
            <span :class="{ activo: reserva.activa }">
              {{ reserva.activa ? 'Activa' : 'Inactiva' }}
            </span>
          </p>

          <button class="btn-eliminar" @click="eliminarReserva(reserva.id)">
            Eliminar
          </button>
        </article>

        <p v-if="reservasFiltradas.length === 0" class="sin-registros">
          No hay reservas registradas.
        </p>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      nombre: '',
      carnet: '',
      cubiculo: '',
      motivo: '',
      reservas: [],
      mensaje: '',
      error: '',
      soloActivas: true,
      contador: 1
    }
  },
  computed: {
    reservasFiltradas() {
      if (this.soloActivas) {
        return this.reservas.filter((reserva) => reserva.activa)
      }
      return this.reservas
    }
  },
  methods: {
    registrarReserva() {
      this.mensaje = ''
      this.error = ''

      if (
        this.nombre.trim() === '' ||
        this.carnet.trim() === '' ||
        this.cubiculo === '' ||
        this.motivo.trim() === ''
      ) {
        this.error = 'Todos los campos son obligatorios.'
        return
      }

      if (this.carnet.trim().length < 5) {
        this.error = 'El carné ingresado no es válido.'
        return
      }

      if (this.motivo.trim().length < 5) {
        this.error = 'El motivo debe tener al menos 5 caracteres.'
        return
      }

      const nuevaReserva = {
        id: this.contador++,
        nombre: this.nombre.trim(),
        carnet: this.carnet.trim(),
        cubiculo: this.cubiculo,
        motivo: this.motivo.trim(),
        activa: true
      }

      this.reservas.push(nuevaReserva)

      this.mensaje = 'Reserva registrada correctamente.'
      this.nombre = ''
      this.carnet = ''
      this.cubiculo = ''
      this.motivo = ''
    },
    eliminarReserva(id) {
      this.reservas = this.reservas.filter((reserva) => reserva.id !== id)
      this.mensaje = 'Reserva eliminada correctamente.'
      this.error = ''
    }
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.contenedor {
  min-height: 100vh;
  background: #f4f7fb;
  color: #1e293b;
  font-family: Arial, sans-serif;
}

.encabezado {
  background: #0f172a;
  color: white;
  text-align: center;
  padding: 30px 20px;
}

.encabezado h1 {
  margin: 0 0 10px;
}

.principal {
  max-width: 1100px;
  margin: 30px auto;
  padding: 0 20px 30px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.panel {
  background: white;
  border-radius: 14px;
  padding: 20px;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.08);
}

.panel h2 {
  margin-top: 0;
  margin-bottom: 15px;
  color: #0f172a;
}

.formulario {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.campo {
  display: flex;
  flex-direction: column;
}

.campo label {
  font-weight: bold;
  margin-bottom: 6px;
}

.campo input,
.campo select,
.campo textarea {
  padding: 10px;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 14px;
}

.campo textarea {
  resize: vertical;
  min-height: 90px;
}

.btn-guardar,
.btn-eliminar {
  border: none;
  border-radius: 8px;
  padding: 10px 14px;
  cursor: pointer;
  font-weight: bold;
}

.btn-guardar {
  background: #2563eb;
  color: white;
}

.btn-guardar:hover {
  background: #1d4ed8;
}

.btn-guardar:disabled {
  background: #94a3b8;
  cursor: not-allowed;
}

.btn-eliminar {
  background: #dc2626;
  color: white;
  margin-top: 10px;
}

.btn-eliminar:hover {
  background: #b91c1c;
}

.mensaje {
  padding: 10px;
  border-radius: 8px;
  margin-bottom: 12px;
  font-weight: bold;
}

.exito {
  background: #dcfce7;
  color: #166534;
}

.error {
  background: #fee2e2;
  color: #991b1b;
}

.filtro {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 15px;
}

.tarjeta {
  border: 1px solid #e2e8f0;
  border-radius: 10px;
  padding: 14px;
  margin-bottom: 12px;
  background: #f8fafc;
}

.tarjeta h3 {
  margin-top: 0;
  margin-bottom: 10px;
}

.activo {
  color: #15803d;
  font-weight: bold;
}

.sin-registros {
  color: #64748b;
  font-style: italic;
}

@media (max-width: 768px) {
  .principal {
    grid-template-columns: 1fr;
  }
}
</style>