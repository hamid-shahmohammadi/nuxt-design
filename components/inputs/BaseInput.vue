<template>
    <div>
        <input
                class="form-control form-control-lg font-14 fw-300"
                :type="inputType"
                :value="value"
                :readonly="readonly"
                :placeholder="placeholder"
                :class="{'is-invalid':form.errors.has(field)}"
                @input="handleInput"
         
            />
            <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has(field)" v-html="form.errors.get(field)" />
    </div>
</template>

<script>
export default {
    props:{
        form:{
            type:Object,
            required:true
        },
        field:{
            type:String,
            required:true
        },
        value:{
            type:String,
            default:''
        },
        placeholder:{
            type:String,
            default:''
        },
        inputType:{
            type:String,
            default:'text'
        },
        readonly:{
            type:Boolean,
            default:false
        }
    },
    methods:{
        handleInput(e){
            this.$emit('input',e.target.value)
        }
    },
    mounted(){
        console.log(this.form.errors)
    }
}
</script>