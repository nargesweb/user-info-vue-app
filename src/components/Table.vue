<template>
    <div class="mt-5">
        <table class="table table-striped border" >
            <thead class="table-primary">
                <tr>
                    <th scope="col">کد</th>
                    <th scope="col">نام</th>
                    <th scope="col">نام خانوادگی</th>
                    <th scope="col">کد ملی</th>
                    <th scope="col">شهر</th>
                    <th scope="col">عملیات</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for=" (item,index) in filtered" :key="index">
                    <td>{{index}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.family}}</td>
                    <td>{{item.code}}</td>
                    <td>{{item.city}}</td>
                    <td>
                        <span class="px-2 text-success fs-5" @click="editUser(index)">
                            <UilEdit class="fs-5" />
                        </span>
                        <span class="px-2 text-danger" @click="deleteItem(index)" >
                            <UilTrash class="fs-5" />
                        </span> 
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="d-flex align-item-center justify-content-center m-5">
            <nav aria-label="Page navigation example">
                <ul class="pagination">
                    <li class="page-item">
                    <a class="page-link" href="#" aria-label="Previous">
                        <span aria-hidden="true">&laquo;</span>
                    </a>
                    </li>
                    <li class="page-item"><a class="page-link" href="#">1</a></li>
                    <li class="page-item"><a class="page-link" href="#">2</a></li>
                    <li class="page-item"><a class="page-link" href="#">3</a></li>
                    <li class="page-item">
                    <a class="page-link" href="#" aria-label="Next">
                        <span aria-hidden="true">&raquo;</span>
                    </a>
                    </li>
                </ul>
            </nav>
        </div>
    </div>
</template>

<script>
// icon 
import { UilTrash } from '@iconscout/vue-unicons'
import { UilEdit } from '@iconscout/vue-unicons'

import eventBus from "../services/eventBus"

export default {
    name: 'NavVueProjectTable',
    components:{
        UilTrash,UilEdit
    },
    methods: {
        deleteItem (index){
            eventBus.$emit("removeUser" , index )
        },
        editUser(index){
            eventBus.$emit("editUser" , index)
        }
    },
    props:{
        filtered : Array
    }
};
</script>

<style scoped>
div{
    text-align: center;
}

</style>