<template>
    <div>
        <b-button  @click="Nuevo()" v-b-tooltip.hover title="Nuevo Registro" variant="primary" ><b-icon icon="plus-circle" aria-hidden="true"></b-icon>Nuevo Registro
        </b-button>
        <table class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>NOMBRE</th>
                    <th>DNI</th>
                    <th>TELEFONO</th>
                    <th>CORREO</th>
                    <th>ACCIONES</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="lista in Listapacientes" :key="lista.PacienteId">
                    <td>{{lista.PacienteId}}</td>
                    <td>{{lista.Nombre}}</td>
                    <td>{{lista.DNI}}</td>
                    <td>{{lista.Telefono}}</td>
                    <td>{{lista.Correo}}</td>
                    <td>
                        <b-button class="m-1" @click="Eliminar(lista.PacienteId)" v-b-tooltip.hover title="Eliminar" variant="danger" ><b-icon icon="trash" aria-hidden="true"></b-icon>
                        </b-button>
                        <b-button class="m-1" @click="Editar(lista.PacienteId)" v-b-tooltip.hover title="Editar" variant="success"><b-icon icon="pen" aria-hidden="true"></b-icon>
                        </b-button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
    <script>
import axios from 'axios'

    export default {
        name:"Dashboard",
        data(){
            return {
                Listapacientes:null,
            }
        },
        components:{
        },
        methods:{
            Nuevo(){
                this.$router.push("/Registrar")
            },   
            Editar(id){
                this.$router.push('/Editar/'+id)
            },
            Eliminar(id){
                if (confirm("¿Eliminar Registro?")) {
                const URL=`https://api.solodata.es/pacientes/%{id}`;
                axios.delete(URL).then(response=>{
                }).catch(error=>{
                console.log('error');
    });
  }
 }
},
    mounted:function(){
            let direccion = "https://api.solodata.es/pacientes?page=1";
            axios.get(direccion).then(response =>{this.Listapacientes = response.data});
 },
}
    
    </script>
    <style scoped>
        .izquierda{text-align: left;}
    </style>