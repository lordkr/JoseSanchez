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
            <tr v-for="elem in props.data" v-bind:key="elem.codigo">
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

<script lang="ts" setup>
import {defineEmits, defineProps, computed, ref, Ref } from "vue"

    const props = defineProps({
        data:{type:Array}
    })

    const emit = defineEmits(['deleteItem'])

    //const itemData:Ref<Array> = ref(props.data)

    const calcular = computed(() => {    
        let result = 0
        props.data.forEach(Element =>{
            result += Element.total
        })    
        return result 
    })

    const deleteI = (id:number) =>{
        emit('deleteItem',id)          
    }
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