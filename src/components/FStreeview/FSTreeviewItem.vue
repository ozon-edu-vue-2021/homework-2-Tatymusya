<template>
    <div>
        <button
            v-if="hasDirChildren"
            class="node-label"
            :class="{active: isOpen}"
            type="button"  
            @click="showHandler()"              
        >
            <node-icon /> {{dirLabel}} - {{parentPath}}
        </button> 
        <span 
            v-else
        >
            {{dirLabel}}
        </span>
        <ul 
            v-if="isOpen"
            class="node-sub-list"
        >
            <li 
                v-for="(item, i) in dirChildren" 
                :key="i"
                class="node-sub-item"
            >
                <fs-treeview-item
                    :items="item"
                    :parent-path="[parentPath, item.name].join('/')"
                />              
            </li>
        </ul>
    </div>
</template>

<script>
import NodeIcon from '@/assets/svg/closed-folder-svgrepo.svg'

export default {
    name: 'fs-treeview-item',
    data() {
        return {
            isOpen: false
        }
    },
    components: {
        NodeIcon
    },
    props: {
        items: {
            type: Object,
            default: () => ({})
        },
        name: {
            type: String,
            default: 'name'
        },
        type: {
            type: String,
            default: 'directory'
        },
        contents: {
            type: String,
            default: 'contents'
        },
        parentPath: {
            type: String,
            default: '~/node_modules'
        }
    },
    computed: {
        dirLabel() {
            return this.items.name;
        },
        dirChildren() {
            return this.items.contents;
        },
        hasDirChildren() {
            return this.items.contents && this.items.contents.length;
        },
    },
    methods: {
        showHandler() {
            this.isOpen = !this.isOpen;
        }
    },
}
</script>

<style scoped>
    .node-sub-list {
        --list-font-face: var(--font-face);
        --list-font-size: var(--font-size);
        --list-primary-color: var(--primary-color);
        --list-base-unit: var(--base-unit);
        --list-double-unit: var(--double-unit);
        --list-active-color: var(--third-color);
        --list-accent-color: var(--accent-color);
        --list-dark-color: var(--secondary-color);
        --list-transition-duration: 0.1s;

        position: relative;
        margin: 0;
        padding: 0 0 0 var(--list-double-unit, 12px);
    }

        @media screen and (prefers-reduced-motion: reduce) {
            .node-label {
                --list-transition-duration: 0s !important;
            }
        }

    .node-sub-item {
        position: relative;
        padding-top: var(--list-base-unit, 6px);
        list-style-type: none;
        font-family: var(--list-font-face);
        font-size: var(--list-font-size);
    }

    .node-label {
        display: flex;
        align-items: center;
        gap: var(--list-base-unit, 6px);
        min-width: 100px;
        padding: var(--list-base-unit, 6px);
        background: var(--list-active-color, #f1f2f3);
        border: none;
        transition-duration: var(--list-transition-duration);
        transition-property: color, border;
    }

    .node-label > svg {
        width: var(--list-double-unit, 12px);
        pointer-events: none;
    }

    .node-label:enabled {
        cursor: pointer;
    }

    @media (hover: hover) {
        .node-label:hover {
            color: var(--list-dark-color, #0c0d0e);
        }
    }

    .active,
    .node-label:active {
        border-bottom: 2px solid var(--list-accent-color, #f48225);
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