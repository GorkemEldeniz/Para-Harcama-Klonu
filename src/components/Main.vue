<template>
    <div class="main">
        
        <h3>{{total.toLocaleString('en-US',{
            style : 'currency',
            currency :'USD'
            })}}$</h3>
        <div class="items">
            <div class="item" v-for="item in data" :key="item.id">
                <img :src="item.pic" :alt="item.name">
                <h5>{{item.name}}</h5>
                <span>{{
                        item.price.toLocaleString('en-US',{
                            style : 'currency',
                            currency : 'USD'
                        })
                    }}</span>
               <div class="shopping" :id="item.id">
                    <span @click="removeItem">-</span>
                    <p>{{item.number}}</p>
                    <span @click="addItem">+</span>
                </div>
            </div>    
        </div>

        <div class="basket" v-if="active">
            <img src="" alt="">
            <h4>Tebrikler!</h4>
            <h4>{{(128000000000 - total)
                .toLocaleString('en-US',{
                    style : 'currency',
                    currency : 'USD'
                })
                }} $ harcandı</h4>
            <div class="products">
               <span  @click="active = !active" >X</span> 
                <!-- <span @click="active = !active">X</span> -->
                <h5>Alınan Ürünler</h5>
                <div class="deneme" v-for="product in newBasket" :key="product">
                    {{product.number}} adet {{product.name}}
                </div>
            </div>
        </div> 

        <footer @click="showBasket">
            Harcamayı Bitir
        </footer>
    </div>
</template>

<script>
import MenuIcon from 'vue-material-design-icons/Menu.vue';
import { watch } from '@vue/runtime-core';
import db from '../db.js';
export default {
    name : 'Main',
    components :{
        MenuIcon
    },
    data(){
        return {
            data : db,
            basket : [],
            counter : 0,
            total : 128_000_000_000,
            active : false,
            newBasket : null
        }
    },
    methods :{
        addItem(e){
            let id = e.target.parentElement.getAttribute('id');
            let item = this.data.find(el => el.id == id);
            //console.log(this.total);
            if(this.total > item.price){
                this.data.forEach(el => el.id == id ? el.number++ : '');
                this.total = this.total - item.price;
                this.basket.push(item);
            }
            //console.log(this.basket);
        },
        removeItem(e){
            let id = e.target.parentElement.getAttribute('id');
            this.data.forEach(el =>  {
                if(el.id == id && el.number >= 1){
                    el.number--
                };
            });
            let item = this.data.find(el => el.id == id);
            //console.log(item.id);
            let index = this.basket.findIndex(el => el.id == item.id);
            if(index != -1){
                this.basket.splice(index,1);
                this.total = this.total + item.price;
            }
            else{
                alert('hata');
            }
        },
        showBasket(){
            this.active = !this.active;
            this.newBasket = new Set(this.basket);    
        }
    }
}   
</script>

<style lang="scss" scoped>
 .main{
     display: flex;
     flex-direction: column;
     width: 90%;
     margin:5rem auto;
     position:relative;
     .basket{
        position:fixed;
        z-index:999;    
        padding:2rem;
        top:0;
        left:0;
        width: 100%;
        height:100vh;
        margin:auto;
        background:var(--white);
        display: flex;
        flex-direction: column;
        color:var(--black);
        align-items: center; 
        h4{
            font-size:2rem;
            font-weight:300;
        }
        .products{
            font-size:1.5rem;
            h5{
                font-size:2rem;
            }
            span{
                position:absolute;
                inset:0;
                margin:2rem;
                cursor:pointer;
            }
        }
     }
     h3{
         font-size:2rem;
         color:var(--black);
         display: inline-flex;
         padding:2rem 0;
         justify-content: center;
         position: sticky;
         top:0;
         border:1px solid #eee;
         left: 0;
         font-weight: 300;
         margin-bottom:2rem;
         background:var(--white);
     }
     .items{
         display: grid;
         grid-template-columns: repeat(4,1fr);
         grid-gap:1rem;
         grid-auto-columns:minmax(0,16rem);
         .item{
             height:23.7rem;
             display: flex;
             flex-direction: column;
             padding: 1rem;
             border:1px solid #eee;
             border-radius: .5rem;
             transition:box-shadow 300ms ease-in;
             &:hover{
                 box-shadow:2px 2px 10px 2px var(--gray);
             }
            img{
                width:16.25rem;
                height: 16.25rem;
                align-self: center;
            }
            h5{
                 font-size:1.2rem;
                 color:var(--black);
            }
            span{
                 color:var(--gray)
            }
            .shopping{
                display:flex;
                justify-content: space-between;
                margin-top:1rem;
                background-color:var(--light);
                border-radius: .4rem;
                padding:.2rem;
                padding:0 1rem;
                span{
                    color:var(--black);
                    cursor: pointer;
                }
            }
        }
     }
    footer{
        position:sticky;
        font-weight: 300;
        bottom:0;
        margin-top:3rem;
        left:0;
        background:linear-gradient(to right,var(--indigo),var(--green));
        font-size:1.1rem;
        height: 3.75rem;
        width: 100%;
        display: flex;
        justify-content:center;
        align-items: center;
        color:var(--white);
        cursor:pointer;
        &:hover{
            color:var(--indigo);
            background:var(--white);
        }
    }
}
</style>