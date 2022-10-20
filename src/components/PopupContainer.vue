<template>
    <div :class="`popupContainer ${position ? 'popupContainer__traingle--' + position : ''}`" :id="id">
        <div class="popupContainer__title">
            <Text2 :color="TEXT_COLORS.DARK">{{ title }}</Text2>
        </div>
        <button :class="`popupContainer__arrow ${position}`" @click="$emit('closeContainer', position, id, true)">
            <Arrow />
        </button>
        <slot />
    </div>
</template>

<script lang="ts">
    import Arrow from '@/assets/svg/Arrow.vue'
    import Text2 from '@/components/Typograpy/Text2.vue'
    import { TEXT_COLORS } from '../components/Typograpy/constants'

    export default {
        components: {
            Arrow, Text2
        },
        props: {
            title: {
                default: '',
                type: String
            },
            position: {
                default: 'left',
                type: String
            },
            id: {
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
            this.$emit('closeContainer', this.position, this.id, false)
        }
    }
</script>

<style lang="scss">
    .popupContainer {
        padding: 42px 38px;
        background: #929292;
        position: relative;
        max-width: 600px;
        &__traingle-- {
            &left {
                background: linear-gradient(-60deg, transparent 25px, #929292 0), linear-gradient(60deg, transparent 25px, transparent 0);
            }
            &right {
                background: linear-gradient(60deg, transparent 25px, #929292 0), linear-gradient(-60deg, transparent 25px, transparent 0);
            }
        }
        &__title {
            margin-bottom: 48px;
        }
        &__arrow {
            background: #1E1E1E;
            border-style: solid;
            border-color: #929292;
            width: 45px;
            height: 45px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: absolute;
            top: 0;
            transition: .4s;
            &:hover {
                transition: .4s;
                cursor: pointer;
                background: rgba(146, 146, 146, .5);
            }
            &.left {
                border-width: 1px 1px 1px 0px;
                right: -45px;
            }
            &.right {
                border-width: 1px 0px 1px 1px;
                left: -45px;
                svg {
                    transform: rotate(180deg);
                }
            }
        }
    }
</style>