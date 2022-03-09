<template>
    <button :class="mode">
        <slot></slot>
    </button>
</template>

<script>
export default {
    props: ['mode']
}
</script>

<style scoped>
.flat {
    background: transparent;
    color: #3a0061;
    border: none;
    box-shadow: none;
    padding: .5rem;
    white-space: nowrap;
}

.flat:hover, .flat:active {
    background: #edd2ff;
}

.btn-purple {
    background: #7a4988;
    color: #FFF;
    border: none;
    box-shadow: none;
    white-space: nowrap;
}

.btn-purple:hover, .btn-purple:active {
    background: #3A0061;
}
</style>
