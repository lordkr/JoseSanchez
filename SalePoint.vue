<template>
    <section class="container">
        <h1>Punto de ventas</h1>
        <div class="item rellenar">
            <div class="formcontrol"><input type="text" v-model="Item.codigo"></div>
            <div class="formcontrol"><input type="text" v-model="Item.producto"></div>
            <div class="formcontrol"><input type="text" v-model="Item.cantidad"></div>
            <div class="formcontrol"><input type="text" v-model="Item.precio"></div>
        </div>
        <div class="formcontrol"><button class="redBtn" @click="addItems">Agregar</button></div>
        <h1>Listado de items</h1>
        <SaleDetail :data="Items" @deleteItem="deleteItems"/>
    </section>
</template>

<script lang="ts" setup>
import SaleDetail from './SaleDetail.vue';
import { Ref, ref } from "vue"
interface ISale {
    codigo:number,
    producto:string,
    cantidad:number,
    precio:number,
    total:number
}
let Item:Ref<ISale> = ref({
    codigo:'',
    producto:'',
    cantidad:'',
    precio:'',    
})
let Items:Ref<Array<ISale>> = ref([])

const addItems = () =>{
    Items.value.push({
        codigo:Item.value.codigo,
        producto:Item.value.producto,
        cantidad:Item.value.cantidad,
        precio:Item.value.precio,
        total:(Item.value.precio*Item.value.cantidad)
    })
       Item.value.codigo=0
       Item.value.producto=''
       Item.value.cantidad=0
       Item.value.precio=0
       Item.value.total=0
}
const deleteItems = (id:number) =>{
    Items.value = Items.value.filter((Item) => Item.codigo !== id)
}
</script>

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.container{    
    display: flex;
    flex-direction: column;
    flex-wrap: wrap; 
    padding: 15px;
    align-content: center;
}
.item{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: space-around;
    
}
.formcontrol{
    padding: 10px;
}
input[type=text] {
    padding: 10px;
    margin: 8px;
    box-sizing: border-box;
    font-size: 16px;
}
input[type=text]:focus {
  border: 3px solid #555;
}
.rellenar{
    background-color: #363637;
}
.redBtn{
    margin: 10px;
    padding: 15px;
    border: none;
    font-size: 16px;
    font-weight: bold;
    text-align: center;    
    background-color: #d33c44;
    color: #fff;
    cursor: pointer;
    border-radius: 5px;
}
.redBtn:hover{
    background-color: #F3252E;    
}
</style>