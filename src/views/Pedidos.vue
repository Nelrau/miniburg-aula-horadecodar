<template>
    <div class="main-container">
        <h1>Pedidos</h1>
        <BurgerForm/>
    </div>
</template>
<script>
import Burgerform from '../components/BurgerForm.vue';

export default {
    name: 'Pedidos',
    components: {
        Burgerform
    }
}
</script>