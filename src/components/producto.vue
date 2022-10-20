<template>
    <div class="container">
        <div class="row">
            <h3>{{producto.nombre}}</h3>
        </div>
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 ">
                <img v-bind:src="producto.imagen" alt="" style="width: 100%">
            </div>
            <div class="col-12 col-sm-6  col-md-8">
                <h6>{{producto.descripción}}</h6>
                <div class="p-3 mb-2 text-white" v-bind:style="colorPrecio">
                    Precio: {{producto.precio}} BOB
                </div>
                <h5>Color</h5>
                <div v-for="d of producto.colores" style="display:inline-block">
                    <span class="color-box clic" v-bind:style=" `background:${d}`"
                        v-on:click.once="obtenerColor(`${d}`)"></span>
                </div>
                <h5>Cantidad</h5>
                <div class="quantity">
                    <button v-on:click="cantidad -= 1">-</button>
                    <div style=" border-radius:5px; border:1px solid #ccc;padding:2px; width: 8%;">{{cantidad}}</div>
                    <button v-on:click="cantidad += 1">+</button>
                </div>
                <div class="buy-box">
                    <button type="button" @click="obtenerDatos()" class="btn btn-primary"
                        :disabled="habilitarDes">Comprar</button>
                </div>

            </div>
        </div>
    </div>

</template>
<script>
export default {
    name: 'producto',
    data() {
        return {
            producto: [],
            colorPrecio: 'background-color: orangered!important; color: white;',
            cantidad: 0,
            color: '',
            habilitar: false,
        }
    },
    methods: {
        getProducto() {
            axios({
                method: "GET",
                url: "http://localhost:4444/Productos?id=1"
            })
                .then(response => {
                    this.producto = response.data[0]
                    console.log(response.data[0].id, 123)
                })

        },
        obtenerColor: function (dato) {
            this.color = dato;
        },
        obtenerDatos: function () {
            if (this.color.length != 0) {
                var valor = [
                    {
                        'id': this.producto.id,
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
        this.getProducto()
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
