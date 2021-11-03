<template>
    <section aria-labelledby="fsStructure">
        <h1 class="visually-hidden" id="fsStructure">My ...</h1>
        <ul class="node-list">
            <li class="node-item">
                <fs-treeview-item 
                    :items="items"
                    :name="'name'"
                    :type="'type'"
                    :contents="'contents'"
                />
            </li>
        </ul>
    </section>
</template>

<script>
import FSTreeviewItem from './FSTreeviewItem.vue';

export default {
    name: 'fs-treeview',
    components: {
        'fs-treeview-item': FSTreeviewItem
    },
    data() {
        return {
        }
    },
    props: {
        items: {
            type: Object,
            required: true,
            default: () => ({})
        }, 
    },
}
</script>

<style scoped>
    .node-list {
        position: relative;
        margin: 0;
        padding: 0;
    }
    .node-item {
        position: relative;
    }
    .visually-hidden,
    .visually-hidden-focusable:not(:focus):not(:focus-within) {
        position: fixed;
        top: 0px;
        left: 0px;
        width: 4px;
        height: 4px;
        opacity: 0;
        overflow: hidden;
        border: none;
        margin: 0;
        padding: 0;
        display: block;
        visibility: visible;
    }
</style>