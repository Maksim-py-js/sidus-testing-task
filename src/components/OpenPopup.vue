<template>
    <div 
        :class="`openPopup ${position}`" 
        :id="`openPopup-${idOpenContainer}`"
        @click="$emit('openContainer', position, idOpenContainer)"
    >
        <Text2 :color="TEXT_COLORS.LIGHT">{{ title }}</Text2>
        <Arrow />
    </div>
</template>

<script lang="ts">
    import Arrow from '@/assets/svg/Arrow.vue'
    import Text2 from '@/components/Typograpy/Text2.vue'
    import { TEXT_COLORS } from '../components/Typograpy/constants'

    export default {
        components: { Arrow, Text2 },
        props: {
            title: {
                default: '',
                type: String
            },
            position: {
                default: 'left',
                type: String
            },
            idOpenContainer: {
                default: '',
                type: String
            },
        },
        data() {
            return {
                TEXT_COLORS: TEXT_COLORS
            }
        },
        mounted() {
            let block:any = document.getElementById(`openPopup-${this.idOpenContainer}`);
            block.style[this.position] = '-' + (block.offsetWidth / 2 - 29) + 'px'
        }
    }
</script>

<style lang="scss">
    .openPopup {
        display: flex;
        align-items: center;
        background: #1E1E1E;
        border-width: 1px 1px 0px 1px;
        border-style: solid;
        border-color: #929292;
        position: absolute;
        top: 50%;
        padding: 10px 12px;
        transition: .4s;
        &:hover {
            cursor: pointer;
            transition: .4s;
            background: rgba(146, 146, 146, .5);
        }
        &.left {
            transform: translateY(-50%) rotate(90deg);
            svg {
                order: -1;
                transform: rotate(90deg);
                margin-right: 17px;
            }
        }
        &.right {
            transform: translateY(-50%) rotate(-90deg);
            svg {
                transform: rotate(90deg);
                margin-left: 17px;
            }
        }
        button {
            background: transparent;
        }
    }
</style>