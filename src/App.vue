<template>
    <div id="app">
        <fs-treeview
            :items="items"
        />
    </div>
</template>

<script>
import FSTreeview from './components/FStreeview/FSTreeview.vue'

export default {
    name: 'App',
    components: {
        'fs-treeview': FSTreeview
    },
    data() {
        return {
            items: {},
        }
    },
    async created() {
        try {
            await fetch('static/node_modules.json')
            .then((val) => val.json())
            .then((val) => {
                this.items = val;
            });

        } catch(err) {
            throw new Error(err);
        }
    },
}
</script>

<style>
@import './assets/css/main.css';

#app {
    --app-font-face: var(--font-face);
    --app-primary-color: var(--primary-color);
    --app-margin: var(--base-unit, 6px);

    margin: var(--app-margin, 12px);
    font-family: var(--app-font-face, 'Avenir, Helvetica, Arial, sans-serif');
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: var(--app-primary-color, #525960);
}
</style>
