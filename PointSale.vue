<template>
    <section class="container">
        <h1>Punto de ventas</h1>
        <div class="item rellenar">
            <div class="formcontrol"><input type="text" v-model="codigo"></div>
            <div class="formcontrol"><input type="text" v-model="producto"></div>
            <div class="formcontrol"><input type="text" v-model="cantidad"></div>
            <div class="formcontrol"><input type="text" v-model="precio"></div>
        </div>
        <div class="formcontrol"><button class="redBtn" @click="addItems">Agregar</button></div>
        <h1>Listado de items</h1>
      <DetailSale :data="Items" @deleteItem="deleteItems"/>
    </section>
</template>

<script lang="ts">
//Option API
import { defineComponent,Ref,ref } from "vue"
import DetailSale from "./DetailSale.vue"
interface IProducto {
    codigo:number,
    producto:string,
    cantidad:number,
    precio:number,
    total:number
}
export default defineComponent({
    name: "SalePoint",
    data() {
        let Items: Ref<Array<IProducto>> = ref([]);
        return {
            Items,
            codigo: 0,
            producto: "",
            cantidad: 0,
            precio: 0,
            total: 0
        };
    },
    methods: {
        addItems(): void {
            this.Items.push({
                codigo: this.codigo,
                producto: this.producto,
                cantidad: this.cantidad,
                precio: this.precio,
                total: (this.precio * this.cantidad)
            });
            this.codigo = 0;
            this.producto = "";
            this.cantidad = 0;
            this.precio = 0;
        },
        deleteItems(id:number){
            this.Items = [... this.Items.filter((item) => item.codigo !== id)]
        }
    },
    components: { DetailSale }
})
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