<template>
    <div class="container">
        <h1 class="title is-spaced">Loading</h1>
        <h2 class="subtitle">A simple loading overlay</h2>
        <hr>

        <div class="content">
            <p>The Loading will be closed after about 10 seconds or by pressing escape or clicking outside</p>
            <button class="button is-primary is-medium" @click="openLoading">Show Loading</button>
        </div>
        <b-loading :active.sync="isLoading" :canCancel="true"></b-loading>
        <pre class="block" v-highlight><code class="html">{{ template1 | pre }}</code></pre>

        <hr>

        <h2 class="title is-spaced">Programmatically opening Loading Overlay</h2>

        <div class="content">
            <p>When you want to close the Loading, call the 'close' method from the component</p>
            <button class="button is-primary is-medium" @click="openProgrammaticallyLoading">Show Loading</button>
        </div>
        <pre class="block" v-highlight><code class="javascript">{{ code2 | pre }}</code></pre>

        <hr>

        <h2 class="title is-spaced">API</h2>
        <b-tabs>
            <b-tab-item label="Properties">
                <b-table :data="props" default-sort="name">
                    <template scope="props">
                        <b-table-column field="name" label="Name">
                            <span v-html="props.row.name"></span>
                        </b-table-column>
                        <b-table-column field="description" label="Description" width="620">
                            <span v-html="props.row.description"></span>
                        </b-table-column>
                        <b-table-column field="type" label="Type">
                            <span>{{ props.row.type }}</span>
                        </b-table-column>
                        <b-table-column field="values" label="Values">
                            <span v-html="props.row.values"></span>
                        </b-table-column>
                        <b-table-column field="default" label="Default">
                            <span v-html="props.row.default"></span>
                        </b-table-column>
                    </template>
                </b-table>
            </b-tab-item>

            <b-tab-item label="Events">
                <b-table :data="events" default-sort="name">
                    <template scope="props">
                        <b-table-column field="name" label="Name">
                            <span v-html="props.row.name"></span>
                        </b-table-column>
                        <b-table-column field="description" label="Description" width="620">
                            <span v-html="props.row.description"></span>
                        </b-table-column>
                        <b-table-column field="parameters" label="Parameters">
                            <span v-html="props.row.parameters"></span>
                        </b-table-column>
                    </template>
                </b-table>
            </b-tab-item>
        </b-tabs>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                isLoading: false,
                props: [
                    {
                        name: '<code>active</code>',
                        description: 'Whether modal is active or not, use the <code>.sync</code> modifier to make it two-way binding',
                        type: 'Boolean',
                        values: '—',
                        default: '<code>false</code>'
                    },
                    {
                        name: '<code>animation</code>',
                        description: 'Custom animation (transition name)',
                        type: 'String',
                        values: '—',
                        default: '<code>fade</code>'
                    },
                    {
                        name: '<code>canCancel</code>',
                        description: `Can close Loading by pressing escape or clicking outside`,
                        type: 'Boolean',
                        values: '—',
                        default: '<code>false</code>'
                    },
                    {
                        name: '<code>onCancel</code>',
                        description: `Callback function to call after user canceled (pressed escape / clicked outside)`,
                        type: 'Function',
                        values: '—',
                        default: '—'
                    }
                ],
                events: [
                    {
                        name: '<code>close</code>',
                        description: 'Triggers when user closed/canceled or called programmatically from the injected component',
                        parameters: '—'
                    }
                ],
                template1: `
                <div class="content">
                    <p>The Loading will be closed after about 10 seconds or by pressing enter or clicking outside</p>
                    <button class="button is-primary is-medium" @click="openLoading">Show Loading</button>
                </div>
                <b-loading :active.sync="isLoading" :canCancel="true"></b-loading>
                `,
                code2: `
                export default {
                    methods: {
                        openProgrammaticallyLoading() {
                            const loadingComponent = this.$loading.open()
                            setTimeout(() => {
                                loadingComponent.close()
                            }, 3 * 1000)
                        }
                    }
                }`
            }
        },
        methods: {
            openLoading() {
                const vm = this
                vm.isLoading = true
                setTimeout(() => {
                    vm.isLoading = false
                }, 10 * 1000)
            },
            openProgrammaticallyLoading() {
                const loadingComponent = this.$loading.open()
                setTimeout(() => {
                    loadingComponent.close()
                }, 3 * 1000)
            }
        }
    }
</script>
