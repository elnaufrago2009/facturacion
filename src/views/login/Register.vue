<template>
  <div>
    <h2 class="pb-4 pt-3">Registro de Empresa</h2>
    <div class="row">
      <div class="col-lg-8">
        <div class="row alert alert-danger" v-show="error.length>2">
          <div class="col">
            {{error}}
          </div>
        </div>
        <!-- FORMULARIO DE REGISTRO -->
        <form v-on:submit.prevent="registrar">

          <!-- Ruc -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Ruc</label>
            <div class="col-sm-5">              
              <div class="input-group mb-2">                
                <input 
                  v-model="empresa.ruc" @input="getRuc"
                  type="number" class="form-control" placeholder="Ruc">
                <div class="input-group-append">
                  <div class="input-group-text"><i class="fa fa-search"></i></div>
                </div>
              </div>
            </div>
          </div>

          <!-- Razon Social -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Razon Social</label>
            <div class="col-sm-7">
              <input
                type="text"
                class="form-control"
                placeholder="Razon Social"
                v-model="empresa.razon">
            </div>
          </div>

          <!-- Dni usuario -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Dni Usuario</label>
            <div class="col-sm-4">              
              <div class="input-group mb-2">                
                <input 
                  v-model="empresa.dni" @input="getDni"
                  type="number" class="form-control" placeholder="DNI">
                <div class="input-group-append">
                  <div class="input-group-text"><i class="fa fa-search"></i></div>
                </div>
              </div>
            </div>
          </div>

          <!-- Nombre usuario -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Nombre Completo</label>
            <div class="col-sm-7">
              <input
                v-model="empresa.nombre"
                type="text" class="form-control" placeholder="Nombre Completo">

            </div>
          </div>

          <!-- Email usuario -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Email</label>
            <div class="col-sm-5">
              <input
                v-model="empresa.email"
                type="email" class="form-control" placeholder="Correo Electronico">
            </div>
          </div>

          <!-- Contrasena usuario -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Contraseña</label>
            <div class="col-sm-5">
              <input
                v-model="empresa.contrasena"
                type="password" class="form-control" placeholder="Contraseña">
            </div>
          </div>

          <!-- Repetir contrasena Usuario -->
          <div class="form-group row">
            <label class="col-sm-3 col-form-label">Repetir Contraseña</label>
            <div class="col-sm-5">
              <input
                v-model="empresa.contrasenna"
                type="password" class="form-control" placeholder="Contraseña">
            </div>
          </div>

          <!-- Enviar -->
          <div class="form-group row">
            <div class="offset-3 col-sm-5">
              <button type="submit" class="btn btn-primary">
                Registrar Empresa
              </button>
            </div>
          </div>


        </form>
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
  var qs = require('qs')
  export default {
    data() {
      return {
        error: '',
        empresa: {
          ruc: '',
          razon: '',
          dni: '',
          nombre: '',
          email: '',
          contrasena: ''
        }
      }
    },
    methods: {
      registrar: function () {
        let post = qs.stringify({empresa: this.empresa});
        axios.post('/apiCliente/login/register.php',post).then(res => {
          if (res.data == 'si'){

          }else{
            this.error = res.data;
          }
          // console.log(res.data)
        })
        // console.log(this.empresa)
      },
      getRuc: function () {
        if (this.empresa.ruc.length == 11){
          axios.post('/apiCliente/helper/ruc.php',qs.stringify({ruc: this.empresa.ruc})).then(res => {
            this.empresa.razon = res.data;                        
          })          
        }
      },
      getDni: function () {
        if (this.empresa.dni.length == 8){
          axios.post('apiCliente/helper/ruc.php',qs.stringify({ruc: this.empresa.dni})).then(res => {
            this.empresa.nombre = res.data;
          })          
        }
      }
    }
  }
</script>