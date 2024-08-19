<template>
    <div>
      <h1>{{ titulo }}</h1>
      <label>Filtro: </label>
      <input type="text" v-model="filtrarNombre" placeholder="Ingrese un nombre..." />
      <h1></h1>
      <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Email</th>
                <th>Dirección</th>
                <th>Teléfono</th>
                <th>Pais</th>
                <th>Ciudad</th>
                <th></th>
            </tr>
            <tr>
                <th><input type="text" v-model="personaNuevaObj.id"></th>
                <th><input type="text" v-model="personaNuevaObj.name"></th>
                <th><input type="text" v-model="personaNuevaObj.email"></th>
                <th><input type="text" v-model="personaNuevaObj.address"></th>
                <th><input type="text" v-model="personaNuevaObj.phone"></th>
                <th><input type="text" v-model="personaNuevaObj.country"></th>
                <th><input type="text" v-model="personaNuevaObj.city"></th>
                <th><button @click="agregarPersona()">AGREGAR</button></th>
            </tr>
            <tr v-if="indexParaEditar !== null">
                <th><input type="text" v-model="personaEditarObj.id"></th>
                <th><input type="text" v-model="personaEditarObj.name"></th>
                <th><input type="text" v-model="personaEditarObj.email"></th>
                <th><input type="text" v-model="personaEditarObj.address"></th>
                <th><input type="text" v-model="personaEditarObj.phone"></th>
                <th><input type="text" v-model="personaEditarObj.country"></th>
                <th><input type="text" v-model="personaEditarObj.city"></th>
                <th><button @click="editarPersona()">GUARDAR</button></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(persona, index) in filtrarPersonas" :key="persona.id">
                <td>{{ persona.id }}</td>
                <td>{{ persona.name }}</td>
                <td>{{ persona.email }}</td>
                <td>{{ persona.address }}</td>
                <td>{{ persona.phone }}</td>
                <td>{{ persona.country }}</td>
                <td>{{ persona.city }}</td>
                <td>
                    <button @click="borrarPersona(index)">BORRAR</button>
                    <button @click="seleccionarPersona(persona, index)">EDITAR</button>
                </td>
            </tr>
        </tbody>
      </table>    
    </div>
  </template>
  
  <script>
  export default {
    name: 'MiComponente',
    data() {
      return {
        titulo: 'Libreta de contactos',
        filtrarNombre: '',
        personaNuevaObj: {
            id: null,
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        personaEditarObj: {
            id: null,
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        indexParaEditar: null,
        personas: [
            {
                id: 1,
                name: "Alice Johnson",
                email: "alice.johnson@example.com",
                address: "123 Maple Street",
                phone: "123-456-7890",
                country: "USA",
                city: "New York"
            },
            {
                id: 2,
                name: "Bob Smith",
                email: "bob.smith@example.com",
                address: "456 Oak Avenue",
                phone: "987-654-3210",
                country: "Canada",
                city: "Toronto"
            },
            {
                id: 3,
                name: "Carol White",
                email: "carol.white@example.com",
                address: "789 Pine Road",
                phone: "555-123-4567",
                country: "UK",
                city: "London"
            },
            {
                id: 4,
                name: "David Brown",
                email: "david.brown@example.com",
                address: "321 Elm Street",
                phone: "444-555-6666",
                country: "Australia",
                city: "Sydney"
            },
            {
                id: 5,
                name: "Emily Davis",
                email: "emily.davis@example.com",
                address: "654 Spruce Lane",
                phone: "333-444-5555",
                country: "USA",
                city: "Los Angeles"
            }
        ]
      }
    },
    components: {
      // Registro de componentes que se utilizaran.
    },
    methods: {
      // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
      agregarPersona() {
        this.personas.push(Object.assign({}, this.personaNuevaObj));
        },

      borrarPersona(index) {
        this.personas.splice(index, 1);     
        },

      editarPersona() {
        this.personas[this.indexParaEditar] = Object.assign({}, this.personaEditarObj);
        this.indexParaEditar = null;
      },

      seleccionarPersona(persona, index) {
        this.indexParaEditar = index;
        this.personaEditarObj = Object.assign({}, persona);	
      }
    },
    computed: {
    filtrarPersonas() {
      const lowercasedFilter = this.filtrarNombre.toLowerCase();
      return this.personas.filter(persona =>
        persona.name.toLowerCase().includes(lowercasedFilter)
      );
    }
    },
    props: {
      // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
  }
  </script>
  
  <style scoped>
  h1 {
    color: #42b983;
  }

  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    padding: 8px;
    border: lpx solid #ddd;
  }

  th {
    background-color: #f2f2f2;
    text-align: center;
  }
  label {
  margin-right: 8px;
}
  </style>