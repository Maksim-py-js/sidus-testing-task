<template>
    <div class="todoList">
        <ul>
            <li v-for="(item, i) in listArray" :key="i" :class="{ isCompleted: item.isCompleted }" @click="$emit('event', item.id)">
                <Text3 :color="TEXT_COLORS.DARK">
                    {{ item.name }}
                </Text3>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
    import Text3 from '@/components/Typograpy/Text3.vue'
    import { TEXT_COLORS } from './Typograpy/constants'

    export default {
        components: { Text3 },
        props: {
            listArray: {
                default() {
                    return []
                },
                type: Array
            }
        },
        data() {
            return {
                TEXT_COLORS: TEXT_COLORS
            }
        }
    }
</script>

<style lang="scss">
    .todoList {
        ul {
            padding-left: 25px;
            margin: 0;
            li {
                &:hover {
                    cursor: pointer;
                }
                &.isCompleted {
                    text-decoration: line-through;
                }
            }
        }
    }
</style>