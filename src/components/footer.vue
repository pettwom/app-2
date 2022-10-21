<template>
    <footer v-bind:style="`background-color: ${footerColor};`">
        <h6>&copy; Petter Meave</h6>
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
