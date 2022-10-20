<template>
    <footer v-bind:style="`background-color: ${footerColor};`">
        <h3>Practica Hecha por Petter Meave</h3>
    </footer>
</template>

<script>
export default {
    name: 'footer_component',
    data() {
        return {
            footerColor: 'slategrey'
        }
    }
}
</script>
