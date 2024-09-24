<template>
    <div id="main-banner">
        <h1>Make You Burger:</h1>
    </div>
</template>
<script>
export default{
    name:'Banner',
    props: ["bannerdata", "bannerburg"]
}
</script>
<style>
#main-banner{
    background-image: url('/public/img/burger.jpg');
    height: 400px;
    background-position: 0 -250px;
    background-size: cover;
    display: flex;
    align-items: center;
}
#main-banner h1{
    font-weight: bold;
    text-align: center;
    background-color: #111;
    color: #fcba03;
    padding: 20px 40px;
    font-size: 45px;

}
</style>