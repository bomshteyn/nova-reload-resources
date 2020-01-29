<template>
        <div>
            <button class="text-center btn btn-primary btn-default" @click="reloadResources">{{ __('Refresh') }}</button>
        </div>
</template>

<script>
export default {
    props: [
        'card',
    ],
    data: () => ({
        'resourceName':null
    }),
    mounted() {
        this.resourceName = this.$router.currentRoute.params.resourceName;
    },
    methods:{
        async reloadResources(){
            if(this.resourceName){
                let filters_backup = _.cloneDeep(this.$store.getters[`${this.resourceName}/filters`]);
                let filters_to_change = _.cloneDeep(filters_backup);
                filters_to_change.push({});
                await this.$store.commit(`${this.resourceName}/storeFilters`,filters_to_change);
                await this.$store.commit(`${this.resourceName}/storeFilters`,filters_backup);
            }
        }
    }
}
</script>
