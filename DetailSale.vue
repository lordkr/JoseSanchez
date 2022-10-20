<template>
  <div>
        <table>
           <thead>
               <tr>
                <th>...</th>
               <th>Codigo</th>
               <th>Producto</th>
               <th>Cant.</th>
               <th>Precio</th>
               <th>Total</th>
              </tr> 
           </thead>
           <tbody>
            <tr v-for="elem in data" v-bind:key="elem.codigo">
                <td><button class="" @click="deleteI(elem.codigo)">Eliminar</button></td>
                <td>{{ elem.codigo}}</td>
                <td>{{ elem.producto}}</td>
                <td>{{ elem.cantidad}}</td>
                <td>{{ elem.precio}}</td>
                <td>{{ elem.total}}</td>

            </tr>
           </tbody>
          <tfoot>
            <td colspan="5">Total</td>
            <td>{{ calcular }}</td>
          </tfoot>
        </table>
    </div>
</template>

<script lang="ts">
//Option API
import { defineComponent } from "vue"
export default defineComponent({
    name:'DetailSale',
    props:['data'],
    //props:{data:{type:Array}},   
    //emits:['deleteItem'], //no es necesario declarar esta seccion
    methods:{
        deleteI: function(id:number) {
        this.$emit('deleteItem',id)                  
    }
    },
    computed: { 
        calcular() {
           let total = 0                    
           //this.data.forEach((element: { cantidad: number; precio: number; total:number}) => {
           this.data.forEach((element: { total:number }) => {
            total += (element.total)
           });           
          return total
        }
    }
})
</script>

<style>
table{ 
    width: 100%;
   border-collapse: collapse; 
}
th, td {  
    padding: 15px;
}
table thead th{
    background-color: #293b4f;
    border:  1px solid #293b4f;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
}
table tbody td {
    border:  1px solid #dddfe1;
    color: #636363;
    text-align: right;
}
table tfoot td {
    text-align: right;
}
</style>