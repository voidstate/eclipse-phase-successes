<script setup>
defineProps( {
    label: {
        type: String,
        required: true,
    },
} )

defineEmits( [ 'clicked' ] )
</script>

<template>
    <div class="control-button">
        <button @click="$emit('clicked')">{{ label }}</button>
    </div>
</template>

<style scoped>
.control-button {
    text-align: center;
    padding-top: 20px;

    button {
        border: 1px solid var(--color-border);
        background-color: var(--color-background-soft);
        padding: .5rem 1rem;
        border-radius: 8px;

        &:hover {
            background-color: var(--indigo);
        }
    }
}

@media (min-width: 1024px) {
    .control-button {
        text-align: unset;
        padding: 0 0 1rem 0;
        position: relative;
        left: -26px;
        top: 20px;

        &:before {
            content: ' ';
            border-left: 1px solid var(--color-border);
            position: absolute;
            bottom: calc(50% + 30px);
            left: 26px;
            height: calc(50% - 10px);
        }
    }
}
</style>