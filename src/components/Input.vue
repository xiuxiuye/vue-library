<style scoped>
.ctsi-input{
    
}
input{
    outline: 0;
    border: 1px solid rgba(220,222,226,0.8);
    background-color: rgba(220,222,226,0.8);
    border-radius: 24px;
    padding-left: 24px; 
}
input:focus{
    border: 1px solid white;
}
</style>

<template>
    <div class="ctsi-input">
        <label :class="[size]">{{label}}</label>
        <input :type="type" :placeholder="placeholder"
            :class="[size]"
            :value="value"
            @input="$emit('input', $event.target.value)">
    </div>
</template>

<script>
export default {
    props: {
        label: {
            type: String,
            default: ''
        },
        type: {
            type: String,
            default: 'text'
        },
        placeholder: {
            type: String,
            default: ''
        },
        size: {
            type: String,
            default: 'normal'
        },
        value: {},
    }
}
</script>