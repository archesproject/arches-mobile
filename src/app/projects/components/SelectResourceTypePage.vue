<template>
<v-ons-page>
    <div>
        <v-ons-list>
            <v-ons-list-item class="resource-model-name-panel" tappable modifier="longdivider" v-for="resource_type in resource_types" :key="resource_type.graphid" @click="selectResourceType(resource_type);">
                <span>
                    <div class='resource-model-name'>
                        <span class="icon-circle" v-bind:style="{ background: [resource_type.color], color: '#fff'}">
                            <v-ons-icon class="resource-model-icon" v-bind:icon="resource_type.iconclass.replace('fa ', '')" v-bind:style="{}"></v-ons-icon>
                        </span>
                        <span class='resource-model-title'>
                            New {{resource_type.name}}
                        </span>
                    </div>
                </span>
            </v-ons-list-item>
        </v-ons-list>
    </div>
</v-ons-page>
</template>

<script>
export default {
    name: 'SelectResourceTypePage',
    data() {
        return {
            state: 'initial'
        };
    },
    computed: {
        resource_types: {
            cache: false,
            get: function() {
                var self = this;
                return self.$store.getters.activeProject.graphs;
            }
        }
    },
    methods: {
        selectResourceType: function(e) {
            this.$store.commit('clearActiveResourceInstance');
            this.$store.commit('setActiveGraphId', e.graphid);
            this.$router.push({
                name: 'resource',
                params: {
                    nodegroupid: null,
                    tabIndex: 1
                }
            });
        }
    }
};
</script>

<style scoped>
.resource-model-name-panel {
    border-bottom: 1px solid #eee;
}
.resource-model-name {
    display: flex;
    flex-direction: row;
}
.resource-model-title {
    display: flex;
    flex-direction: column;
    padding-left: 5px;
    color: #271F4C;
    font-size: 14px;
    margin-top: 10px;
}
.resource-model-icon {
    text-align: center;
    vertical-align: 5px;
    font-size: 14px;
    padding: 10px 0 12px 0;
    width: 100%;
}
.icon-circle {
    box-sizing: border-box;
    border: solid 1px #1B48DD;
    border-radius: 50%;
    height: 36px;
    width: 36px;
    background: #d7e0f8;
}
</style>
