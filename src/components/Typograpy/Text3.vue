<template>
    <p :class="`text-3 ${color}`">
        <slot/>
    </p>
</template>

<script lang="ts">
import { TEXT_COLORS } from './constants'
export default {
    props: {
        color: {
            default: TEXT_COLORS.LIGHT,
            type: String
        }
    }
}
</script>

<style lang="scss">
    .text-3 {
        margin: 0;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 26px;
        &.light {
            color: #D9D9D9;
        }
        &.dark {
            color: #1E1E1E;
        }
    }
</style>