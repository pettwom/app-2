<template>
    <div class="about">
        <producto_component />
        <tarjetas_component />
    </div>
</template>

<script>
import producto_component from '@/components/producto.vue'
import tarjetas_component from '@/components/tarjetas.vue'

export default {
    name: 'about',
    components: {
        producto_component,
        tarjetas_component
    }
}
</script>
