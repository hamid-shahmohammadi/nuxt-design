<template>
<div class="setting-block">
    <div class="setting-title">Designs</div>
    <div class="setting-body white-bg-color">
        <table class="table table-stribed">
            <thead>
                <tr>
                    <td></td>
                    <td>Title</td>
                    <td>Status</td>
                    <td>Actions</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="design in designs" :key="design.id">
                    <td>
                        <div v-if="design.images">
                            <img :src="design.images.thumbnail" width="100" />
                        </div>
                    </td>
                    <td>{{design.title}}</td>
                    <td>{{design.is_live ? 'Published':'Draf'}}</td>
                    <td>
                        <nuxt-link :to="{name:'designs.edit',params:{id:design.id}}">Edit</nuxt-link>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</div>
</template>

<script>
export default{
    middleware:['auth'],
    data(){
        return {
            designs:[]
        }      
    },
    methods:{
        async fetchUserDesigns(){
            console.log(this.$auth.user.data.id)
            const {data}=await this.$axios.$get(
                `/users/${this.$auth.user.data.id}/designs`
            );
            console.log(data)
            this.designs=data;
        }
    },
    created(){
        this.fetchUserDesigns();
    }
}
</script>