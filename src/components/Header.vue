<template>
   <header>
       <h1>
           <span>#</span>128MilyarDolarNerede
       </h1>
   </header>
</template>

<script>
export default {
    name : 'Header'
}
</script>

<style lang="scss" scoped>
header{
    width: 100%;
    background:#fff;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 4.3rem;
    h1{
        font-size:2rem;
        color:#000;
        span{
            color:var(--indigo);
        }
    }
}
</style>