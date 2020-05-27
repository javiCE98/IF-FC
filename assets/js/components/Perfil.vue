<template>
    <div class="mt-5 text-center">
        <b-container>
            <b-button variant="info" disabled v-if="!usuario.fechaNacimiento">
                <b-spinner small type="grow"></b-spinner>
                Cargando...
            </b-button>
            <b-card
                header="Mi perfil"
                header-text-variant="white"
                header-tag="header"
                header-bg-variant="info"
                style="max-width: 40rem;"
                v-if="usuario.fechaNacimiento"
            >
                <h3 v-if="!editar">{{ usuario.nombre }} {{ usuario.apellidos }}</h3>

                <b-row class="mb-2" v-if="editar">
                    <b-col>
                        <strong class="text-dark">Nombre:</strong>
                    </b-col>
                    <b-col>
                        <b-form-input name="usuario.nombre" id="userName" ref="usuarioNombre" v-model="usuario.nombre"></b-form-input>
                        <span id="nombreError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2" v-if="editar">
                    <b-col>
                        <strong class="text-dark">Apellidos:</strong>
                    </b-col>
                    <b-col>
                        <b-form-input v-model="usuario.apellidos" id="usuarioApellidos"></b-form-input>
                        <span id="apellidosError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2">
                    <b-col>
                        <strong class="text-dark">Email:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.email }}
                    </b-col>
                     <b-col v-if="editar">
                        <b-form-input v-model="usuario.email" id="usuarioEmail"></b-form-input>
                        <span id="emailError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2" v-if="editar">
                    <b-col>
                        <strong class="text-dark">Contraseña:</strong>
                    </b-col>
                     <b-col>
                        <b-form-input type="password" v-model="usuario.password" id="usuarioPassword"></b-form-input>
                        <span id="passwordError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2" v-if="editar">
                    <b-col>
                        <strong class="text-dark">Confirmar contraseña:</strong>
                    </b-col>
                     <b-col>
                        <b-form-input type="password" v-model="confirmarPass" id="confirmPass"></b-form-input>
                        <span id="confirmPasswordError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2" v-if="editar">
                    <b-col>
                        
                    </b-col>
                     <b-col>
                        <strong class="text-dark">Ver contraseñas</strong>
                        <b-form-checkbox id="showPasswords"></b-form-checkbox>
                        
                    </b-col>
                </b-row>


                <b-row class="mb-2">
                    <b-col>
                        <strong class="text-dark">Dni:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.dni }}
                    </b-col>
                     <b-col v-if="editar">
                        <b-form-input v-model="usuario.dni" id="usuarioDni"></b-form-input>
                        <span id="dniError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2">
                    <b-col>
                        <strong class="text-dark">Fecha de nacimiento:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.fechaNacimiento.date.substring(0,10)}}                       
                    </b-col>
                     <b-col v-if="editar">
                        <b-form-input type="date" v-model="fecha" id="date"></b-form-input>
                    </b-col>
                </b-row>

                <hr><span class="text-info mb-5">Dirección</span>

                <b-row class="mb-2 mt-2">
                    <b-col>
                        <strong class="text-dark">Calle:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.calle }}
                    </b-col>
                     <b-col v-if="editar">
                        <b-form-input v-model="usuario.calle" id="usuarioCalle"></b-form-input>
                        <span id="calleError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2">
                    <b-col>
                        <strong class="text-dark">Localidad:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.localidad }}
                    </b-col>
                     <b-col v-if="editar">
                        <b-form-input v-model="usuario.localidad" id="usuarioLocalidad"></b-form-input>
                        <span id="localidadError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2">
                    <b-col>
                        <strong class="text-dark">Provincia:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.provincia }}
                    </b-col>
                    <b-col v-if="editar">
                        <b-form-input v-model="usuario.provincia" id="usuarioProvincia"></b-form-input>
                        <span id="provinciaError"></span>
                    </b-col>
                </b-row>

                <b-row class="mb-2">
                    <b-col>
                        <strong class="text-dark">Código postal:</strong>
                    </b-col>
                    <b-col v-if="!editar">
                        {{ usuario.cp }}
                    </b-col>
                    <b-col v-if="editar">
                        <b-form-input v-model="usuario.cp" id="usuarioCp"></b-form-input>
                        <span id="cpError"></span>
                    </b-col>
                </b-row>

                <b-row class="mt-3">
                    <b-col>
                        <b-button variant="outline-primary" v-if="!editar" @click="editarPerfil">Editar</b-button>
                        <b-button variant="outline-success" v-if="editar" id="saveChanges" @click="actualizarPerfil(usuario.nombre, usuario.apellidos, usuario.email, fecha, usuario.password, usuario.dni, usuario.calle, usuario.localidad, usuario.provincia, usuario.cp)">Actualizar</b-button>
                        <b-button variant="outline-danger" v-if="editar" @click="editar = false">Cancelar</b-button>
                    </b-col>
                </b-row>
                
            </b-card>
        </b-container>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        data: () => ({
            usuario: [],
            editar: false,
            fecha: '',
            confirmarPass: ''
        }),
        mounted () {
            axios
                .get('/misdatos')
                .then(response => (
                    this.usuario = response.data
                ))
        },
        methods: {
            editarPerfil(){
                this.editar = true;
                this.fecha = this.usuario.fechaNacimiento.date.substring(0,10)


                this.$nextTick(function () {
                document.querySelector('body').style.cursor = "pointer";
                const usuarioNombre = document.getElementById("userName");
                const usuarioApellidos = document.getElementById("usuarioApellidos");
                const usuarioEmail = document.getElementById("usuarioEmail");
                const usuarioPassword = document.getElementById("usuarioPassword");
                const confirmarPassword = document.getElementById("confirmPass");
                const usuarioDni = document.getElementById("usuarioDni");
                const usuarioCalle = document.getElementById("usuarioCalle");
                const usuarioLocalidad = document.getElementById("usuarioLocalidad");
                const usuarioProvincia = document.getElementById("usuarioProvincia");
                const usuarioCp = document.getElementById("usuarioCp");
                const showPasswords = document.getElementById("showPasswords");
                const botonSave = document.getElementById("saveChanges");

                const nombreError = document.getElementById("nombreError");
                const apellidosError = document.getElementById("apellidosError");
                const emailError = document.getElementById("emailError");
                const passwordError = document.getElementById("passwordError");
                const confirmPasswordError = document.getElementById("confirmPasswordError");
                const dniError = document.getElementById("dniError");
                const calleError = document.getElementById("calleError");
                const localidadError = document.getElementById("localidadError");
                const provinciaError = document.getElementById("provinciaError");
                const cpError = document.getElementById("cpError");

                console.log(this.usuario.password);
                this.usuario.password = null;
                console.log(this.usuario.password);

                if(confirmarPassword.value == ""){
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                }
                else{
                            saveChanges.style.cursor = "pointer";
                            saveChanges.disabled = false;
                }

                document.getElementById("showPasswords").onclick = () => {
                if(document.getElementById("showPasswords").checked) {
                        console.log('checked');
                        document.getElementById("usuarioPassword").type = "text";
                        document.getElementById("confirmPass").type = "text";
                    }

                    else{
                        console.log('not checked');
                        document.getElementById("usuarioPassword").type = "password";
                        document.getElementById("confirmPass").type = "password";
                    }

                }
                
                

                nombreError.innerHTML = "";
                document.getElementById("userName").onkeyup = () => {
                    const regExpNombre =/[A-Za-z]/;
                    if(regExpNombre.test(usuarioNombre.value)){
                        nombreError.innerHTML = "";
                        usuarioNombre.style.borderColor = "";
                        saveChanges.style.cursor = "pointer";
                        saveChanges.disabled = false;
                    }
                    if(!regExpNombre.test(usuarioNombre.value)){
                        nombreError.style.color = "red";
                        nombreError.innerHTML = "El campo debe tener una cadena de caracteres";
                        usuarioNombre.style.borderColor = "red";
                        saveChanges.style.cursor = "not-allowed";
                        saveChanges.disabled = true;
                        
                    }
                    if(usuarioNombre.value == ""){
                        nombreError.style.color = "red";
                        nombreError.innerHTML = "El campo no puede estar vacío";
                        usuarioNombre.style.borderColor = "red";
                        saveChanges.style.cursor = "not-allowed";
                        saveChanges.disabled = true;
                    }
                }

                    apellidosError.innerHTML = "";
                    usuarioApellidos.onkeyup = () => {
                        const regExpApellidos =/[A-Za-z]/;
                                    
                        if(regExpApellidos.test(usuarioApellidos.value)){
                            apellidosError.innerHTML = "";
                            usuarioApellidos.style.borderColor = "";
                            saveChanges.style.cursor = "pointer";
                            saveChanges.disabled = false;
                        }
                        if(!regExpApellidos.test(usuarioApellidos.value)){
                            apellidosError.style.color = "red";
                            apellidosError.innerHTML = "El campo debe tener una cadena de caracteres";
                            usuarioApellidos.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                        }
                        if(usuarioApellidos.value == ""){
                            apellidosError.style.color = "red";
                            apellidosError.innerHTML = "El campo no puede estar vacío";
                            usuarioApellidos.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                        }
                    }

                    
                    dniError.innerHTML = "";
                    usuarioDni.onkeyup = () => {
                        const regExpDni =/^[0-9]{8}[TRWAGMYFPDXBNJZSQVHLCKE]$/i;
                        if(regExpDni.test(usuarioDni.value)){
                            dniError.innerHTML = "";
                            usuarioDni.style.borderColor = "";
                            saveChanges.style.cursor = "pointer";
                            saveChanges.disabled = false;
                        }
                        if(!regExpDni.test(usuarioDni.value)){
                            dniError.style.color = "red";
                            dniError.innerHTML = "El campo debe contener 8 números y 1 letra";
                            usuarioDni.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                        }
                        if(usuarioDni.value == ""){
                            dniError.style.color = "red";
                            dniError.innerHTML = "El campo no puede estar vacío";
                            usuarioDni.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                        }
                    }

                    emailError.innerHTML = "";
                    usuarioEmail.onkeyup = () => {
                        const regExpEmail =/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.([a-zA-Z]{2,4})+$/;
                        if(regExpEmail.test(usuarioEmail.value)){
                            emailError.innerHTML = "";
                            usuarioEmail.style.borderColor = "";
                            saveChanges.style.cursor = "pointer";
                            saveChanges.disabled = false;
                        }
                        if(!regExpEmail.test(usuarioEmail.value)){
                            emailError.style.color = "red";
                            emailError.innerHTML = "El campo debe tener formato email";
                            usuarioEmail.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                        }
                        if(usuarioEmail.value == ""){
                            emailError.style.color = "red";
                            emailError.innerHTML = "El campo no puede estar vacío";
                            usuarioEmail.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                        }
                    }

                    confirmPasswordError.innerHTML = "";
                        confirmarPassword.onkeyup = () => {
                        if(confirmarPassword.value != usuarioPassword.value){
                            confirmPasswordError.style.color = "red";
                            confirmPasswordError.innerHTML = "Las contraseñas no coinciden";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                            confirmarPassword.style.borderColor = "red";
                        }
                        else{
                            confirmPasswordError.innerHTML = "";
                            saveChanges.style.cursor = "pointer";
                            saveChanges.disabled = false;
                            confirmarPassword.style.borderColor = "";
                        }
                    }

                    calleError.innerHTML = "";
                        usuarioCalle.onkeyup = () => {
                            const regExpCalle =/[A-Za-z]/;
                            if(regExpCalle.test(usuarioCalle.value)){
                                calleError.innerHTML = "";
                                usuarioCalle.style.borderColor = "";
                                saveChanges.style.cursor = "pointer";
                                saveChanges.disabled = false;
                            }
                            if(!regExpCalle.test(usuarioCalle.value)){
                                calleError.style.color = "red";
                                calleError.innerHTML = "El campo debe tener una cadena de caracteres";
                                usuarioCalle.style.borderColor = "red";
                                saveChanges.style.cursor = "not-allowed";
                                saveChanges.disabled = true;
                            }
                            if(usuarioCalle.value == ""){
                                calleError.style.color = "red";
                                calleError.innerHTML = "El campo no puede estar vacío";
                                usuarioCalle.style.borderColor = "red";
                                saveChanges.style.cursor = "not-allowed";
                                saveChanges.disabled = true;
                            }
                        }

                        localidadError.innerHTML = "";
                        usuarioLocalidad.onkeyup = () => {
                           const regExpLocalidad =/[A-Za-z]/;
                           if(regExpLocalidad.test(usuarioLocalidad.value)){
                              localidadError.innerHTML = "";
                              usuarioLocalidad.style.borderColor = "";
                              saveChanges.style.cursor = "pointer";
                              saveChanges.disabled = false;
                           }
                           if(!regExpLocalidad.test(usuarioLocalidad.value)){
                               localidadError.style.color = "red";
                              localidadError.innerHTML = "El campo debe tener una cadena de caracteres";
                              usuarioLocalidad.style.borderColor = "red";
                              saveChanges.style.cursor = "not-allowed";
                              saveChanges.disabled = true;
                           }
                           if(usuarioLocalidad.value == ""){
                               localidadError.style.color = "red";
                              localidadError.innerHTML = "El campo no puede estar vacío";
                              usuarioLocalidad.style.borderColor = "red";
                              saveChanges.style.cursor = "not-allowed";
                              saveChanges.disabled = true;
                           }
                       }

                        provinciaError.innerHTML = "";
                        usuarioProvincia.onkeyup = () => {
                           const regExpLocalidad =/[A-Za-z]/;
                           if(regExpLocalidad.test(usuarioProvincia.value)){
                               provinciaError.innerHTML = "";
                               usuarioProvincia.style.borderColor = "";
                               saveChanges.style.cursor = "pointer";
                               saveChanges.disabled = false;
                            }
                            if(!regExpLocalidad.test(usuarioProvincia.value)){
                                provinciaError.style.color = "red";
                               provinciaError.innerHTML = "El campo debe tener una cadena de caracteres";
                               usuarioProvincia.style.borderColor = "red";
                               saveChanges.style.cursor = "not-allowed";
                               saveChanges.disabled = true;
                            }
                            if(usuarioProvincia.value == ""){
                                provinciaError.style.color = "red";
                              provinciaError.innerHTML = "El campo no puede estar vacío";
                              usuarioProvincia.style.borderColor = "red";
                              saveChanges.style.cursor = "not-allowed";
                              saveChanges.disabled = true;
                            }
                        }

                        cpError.innerHTML = "";
                        usuarioCp.onkeyup = () => {
                          const regExpCp =/^(?:0[1-9]\d{3}|[1-4]\d{4}|5[0-2]\d{3})$/;
                          if(regExpCp.test(usuarioCp.value)){
                            cpError.innerHTML = "";
                            usuarioCp.style.borderColor = "";
                            saveChanges.style.cursor = "pointer";
                            saveChanges.disabled = false;
                          }
                          if(!regExpCp.test(usuarioCp.value)){
                            cpError.style.color = "red";
                            cpError.innerHTML = "El campo debe tener 5 numeros comprendidos entre 01000 y 52999";
                            usuarioCp.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                          }
                          if(usuarioCp.value == ""){
                            cpError.style.color = "red";
                            cpError.innerHTML = "El campo no puede estar vacío";
                            usuarioCp.style.borderColor = "red";
                            saveChanges.style.cursor = "not-allowed";
                            saveChanges.disabled = true;
                         }
                       }

                })
                










            },
            actualizarPerfil(nombreEdit, apellidosEdit, emailEdit, fechaedit, passEdit, dniEdit, calleEdit, localidadEdit, provinciaEdit, cpEdit){
                var ruta = '/editar-datos'


                $.ajax({
                    type: 'PUT',
                    url: ruta,
                    data: ({nombre: nombreEdit,
                            apellidos: apellidosEdit,
                            email: emailEdit,
                            fecha: fechaedit,
                            pass: passEdit,
                            dni: dniEdit,
                            calle: calleEdit,
                            localidad: localidadEdit,
                            provincia: provinciaEdit,
                            cp: cpEdit
                            }),
                    async: true,
                    dataType: 'json',
                    success: function (data) {
                        console.log(data);
                        this.usuario = data
                    }
                }) 
                if (location.reload(true)) {
                    this.editar = false;
                }



            }
        }
    }
</script>