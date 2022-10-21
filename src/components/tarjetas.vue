<template>
    <hr>
    <div class="container ">
        <div class=" callout shadow p-3 mb-5 bg-body rounded">
            <div class="row">
                <h3>{{nombreR}}</h3>
            </div>
            <div class="row">
                <div class="col-12 col-sm-6 col-md-4 ">
                    <img v-bind:src="imagenR" alt="" style="width: 100%">
                </div>
                <div class="col-12 col-sm-6  col-md-8">
                    <h6>{{descripcionR}}</h6>
                    <div class="p-3 mb-2 text-white" v-bind:style="colorPrecio">
                        Precio: {{precioR}} BOB
                    </div>
                    <h5>Color</h5>
                    <div v-for="d of coloresR" style="display:inline-block">
                        <span class="color-box clic" v-bind:style=" `background:${d}`"
                            v-on:click.once="obtenerColor(`${d}`)"></span>
                    </div>
                    <h5>Cantidad</h5>
                    <div class="quantity">
                        <button v-on:click="cantidad -= 1">-</button>
                        <div style=" border-radius:5px; border:1px solid #ccc;padding:2px; width: 8%;">{{cantidad}}
                        </div>
                        <button v-on:click="cantidad += 1">+</button>
                    </div>
                    <div class="buy-box">
                        <button type="button" @click="obtenerDatos()" class="btn btn-primary"
                            :disabled="habilitarDes">Comprar</button>
                    </div>

                </div>
            </div>
        </div>
        <div class="row">
            <h4>Productos relacionados</h4>
        </div>
        <div class="row">
            <div class="col" style="display: flex" v-if="tarjetas!=''">

                <div class="card" style="width: 18rem; margin:15px;" v-for="v of tarjetas">
                    <div class="card-body">
                        <h5 class="card-title">{{v.nombre}}</h5>
                        <img v-bind:src="v.imagen" alt="" style="width: 100%;">
                        <p class="card-text">{{v.descripción}}</p>
                        <div class="producto-relacionado-precio">Precio: {{v.precio}} BOB</div>
                        <div v-for="d of v.colores" style="display: inline-block">
                            <div class="color-box" v-bind:style="`background: ${d}`"></div>
                        </div>
                        <div class="d-grid gap-2" style="position: relative; bottom: 0;">
                            <a v-on:click="recuperarTarjeta(`${v.id}`)" class="btn btn-success">Comprar</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { assertExpressionStatement } from '@babel/types';

export default {
    name: 'tarjetas_components',
    data() {
        return {
            tarjetas: [],
            imagenR: '',
            nombreR: '',
            descripcionR: '',
            precioR: 0,
            coloresR: [],
            cantidad: 0,
            color: '',
            habilitar: false,
            colorPrecio: 'background-color: orangered!important; color: white;',
        }
    },
    methods: {
        getTarjetas() {
            axios({
                methods: 'GET',
                url: 'http://localhost:4444/Productos'
            })
                .then(response => {
                    this.tarjetas = response.data
                    console.log(this.tarjetas, 654)
                })
        },
        recuperarTarjeta(id) {
            console.log(id)
            axios({
                methods: 'GET',
                url: 'http://localhost:4444/Productos/?id=' + id
            })
                .then(response => {
                    this.imagenR = response.data[0].imagen
                    this.nombreR = response.data[0].nombre
                    this.descripcionR = response.data[0].descripción
                    this.precioR = response.data[0].precio
                    this.coloresR = response.data[0].colores
                })
        },
        obtenerColor: function (dato) {
            this.color = dato;
        },
        obtenerDatos: function () {
            if (this.color.length != 0) {
                var valor = [
                    {
                        'cantidad': this.cantidad,
                        'color': this.color
                    }
                ]
                console.log(valor)
                alert(JSON.stringify(valor))
            } else {
                alert('debe seleccionar un color')
            }
        }
    },
    mounted() {
        this.getTarjetas()
    },
    computed: {
        habilitarDes() {
            if (this.cantidad <= 0) {
                this.habilitar = true
            } else {
                this.habilitar = false
            }
            return this.habilitar
        }
    }
}
</script>
