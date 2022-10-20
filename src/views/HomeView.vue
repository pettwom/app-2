<template>
    <div class="home">
        <inicio_component />
        <producto_component />
    </div>
</template>

<script>
import inicio_component from '@/components/inicio.vue'
import producto_component from '@/components/producto.vue'
export default {
    name: 'HomeView',
    components: {
        inicio_component,
        producto_component
    }
}
</script>
