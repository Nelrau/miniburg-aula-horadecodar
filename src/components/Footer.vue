<template>
    <div>
        <footer id="footer">
            <p>Make your burger &copy;2024</p>
        </footer>
    </div>
</template>
<script>
export default {
    name: 'Footer'
}
</script>
<style>
#footer{
    height: 100px;
    background-color: #222;
    border-top:4px solid #111;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fcba03;
    bottom: 0;
    width:100%;
}
</style>