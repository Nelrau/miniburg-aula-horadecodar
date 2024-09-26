<template>
    <div id="mensage">
        <p>{{ msg }} </p>
    </div>
</template>
<script>
export default{
    name:'Message',
    props:{
        msg: String
    },

}
</script>
<style scoped>
#mensage{
    background-color: aqua;
    color: blue;
    border: 2px solid #02baff;
    border-radius: 7px;
    width: 500px;
    max-width: 400px;
    margin:30px auto;
}
#mensage p{
    text-align: center;
}
</style>