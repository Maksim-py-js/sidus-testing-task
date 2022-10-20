<template>
    <button class="button" @click="$emit('clickButton')">
        <slot />
    </button>
</template>

<script lang="ts">
export default {
    
}
</script>

<style lang="scss">
    .button {
        background: #1E1E1E;
        border-radius: 5px;
        padding: 9px;
        border: none;   
        &:hover {
            cursor: pointer;
        }
    }
</style>