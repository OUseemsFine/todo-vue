<template>
<form @submit.prevent.lazy.trim="onSubmit">
    <label for="new-todo-input">
        What needs to be done?
    </label>
    <input 
    type="text"
    id="new-todo-input"
    name="new-todo"
    autocomplete="off"
    v-model="label"
    />
    <button type="submit">
        Add
    </button>
</form>
</template>

<script>
export default{
    method:{
        onSubmit(){

            console.log('Label value: ', this.label);
        },
    },
    data(){
        return{
            label:"",
        };
    },
};
</script>