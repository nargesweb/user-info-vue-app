<template>
    <div class="">
        <nav class="navbar navbar-light bg-light border">
        <div class="container-fluid align-items-center">
            <a class="navbar-brand text-black-50" >
                <p><UilListOlAlt/> <span class=" text-primary">فهرست ثبت قطعات</span> </p>
            </a>
            <button class="btn btn-outline-primary rounded-pill"  @click="openingAddItem"> ثبت قطعه جدید</button>
        </div>
        </nav>
    </div>
</template>

<script>
// icon 
import { UilListOlAlt } from '@iconscout/vue-unicons';

import eventBus from "../services/eventBus.js"

export default {
    name: 'NavVueProjectHeader',
    methods: {
        openingAddItem(){
            eventBus.$emit("openAddItem") 
        }
    },
    components:{
        UilListOlAlt,
    },
    props:{
      
    }
};
</script>

<style scoped>

</style>