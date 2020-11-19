<template>
    <div>
        <Header />
            <div class="container">
                

                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Raza</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="raza" id="raza" v-model="form.raza">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Fecha</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="fecha" id="fecha" v-model="form.fecha">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">Estado</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="estado" id="estado" v-model="form.estado">
                            </div>
                        </div>
                    </div>
                    <div class="form-group left row">
                         <div class="col">
                            <label for="" class="control-label col-sm-2">Peso</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="peso" id="peso" v-model="form.peso">
                            </div>
                          </div>
                         <div class="col">
                              <label for="" class="control-label col-sm-2">Corporal</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="corporal" id="corporal" v-model="form.corporal">
                              </div>
                        </div>
                    </div>
                    <div class="form-group left row ">
                        <div class="col">
                              <label for="" class="control-label col-sm-2">Nacimiento</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="nacimiento" id="nacimiento" v-model="form.nacimiento">
                            </div>
                        </div>
                        
                    </div>


                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>


            </div>
        <!-- <Footer /> -->

    </div>
</template>
<script>
import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return {
            form:{
                "raza" : "",
                "fecha": "", 
                "estado" : "",
                "peso" :"",
                "corporal" : "",
                "nacimiento" : "",
                "token" : "" 
            }
        }
    },
    components:{
        Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token");
            axios.post("http://localhost/apirest_bovino/bovinos",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Bovino creado","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
        
    }
}
</script>
<style scoped>
.left{
    text-align:  left;
}
</style>