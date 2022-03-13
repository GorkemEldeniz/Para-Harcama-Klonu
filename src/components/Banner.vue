<template>
    <div class="banner">
        <div class="article">
            <h3>#128MilyarDolarNerede</h3>
            <p>128 milyar doların aniden kayboluyorsa ya çok başarılı bir sihirbazın gösterisindesiniz 
                ya da Türkiye'de yaşıyorsunuz
            </p>
            <p>128 Milyar Doları Hemen Harcamaya Başla</p>
        </div>
        <img src="../assets/banner.png" alt="banner">
    </div>
</template>

<script>
export default {
    name : 'Banner'
}
</script>

<style lang="scss" scoped>
    .banner{
        width: 75%;
        margin:5rem auto;
        display: flex;
        gap:1rem;
        background:linear-gradient(to right,var(--indigo),var(--green));
        border-radius: 1rem;
        padding:1rem;
        img{
            width:50%;
            height: 10%;
            object-fit:cover;
        }
        .article{
            width: 50%;
            color:var(--white);
            margin:3rem;
            display: flex;
            gap:3rem;
            align-items:left;
            flex-direction: column;
            h3{
                font-size:2.5rem;
            }
            p{
                font-size:1.5rem;
                &:last-child{
                    margin-top:1rem;
                }
            }    
        }
    }
</style>