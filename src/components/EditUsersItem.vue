<template>
    <div>
        <div class="d-flex align-item-center justify-content-center translate-middle shadow-lg" id="card" >
        <form class ="card p-4 rounded-3" onSubmit="return false">
            <div class="mb-5">
                <button class="position-absolute close-btn btn btn-outline-secondary rounded-circle p-1 d-flex align-item-center justify-content-center mb-3"  @click="openingEditItem"><UilTimes /></button>
            </div>
            <h3 class="mb-4">ویرایش </h3>
            <div class="mb-3">
                <label for="name" class="form-label">نام :</label>
                <input type="text" class="form-control" id="name" v-model="name">
            </div>
            <div class="mb-3">
                <label for="name" class="form-label"> نام خانوادگی :</label>
                <input type="text" class="form-control" id="name" v-model="family" >
            </div>
            <div class="mb-3">
                <label for="name" class="form-label">کد ملی :</label>
                <input type="number" class="form-control" id="name" v-model="code" >
            </div>
            <div class="mb-4">
                <label for="name" class="form-label"> شهر :</label>
                <input type="text" class="form-control" id="name" v-model="city" >
            </div>
            <button type="submit" class="btn btn-primary" @click="replaceData">Submit</button>
            
        </form>
    </div>
    </div>
</template>

<script>
// icon 
import { UilTimes } from '@iconscout/vue-unicons'

import eventBus from "../services/eventBus"
export default {
    name: 'Edit-Users-item',

    data() {
            return {
            name:"",
            family:"",
            city:"",
            code:"",
        };
        
    },
    created() {
        this.name = this.editData.name
        this.family = this.editData.family
        this.city = this.editData.city
        this.code = this.editData.code
    },

    methods: {
        openingEditItem(){
            eventBus.$emit("openEdit")
        },
        replaceData(){
             if(this.name == "" || this.family == "" ||this.code == "" || this.city == ""){
                alert("جدول را کامل کنید ")
            }else{
                eventBus.$emit("editingUser",{name:this.name,family :this.family,code :this.code,city :this.city});
                this.name = ""
                this.family = ""
                this.code = ""
                this.city = ""
                this.openingEditItem();
            }
        }
    },
    components:{
        UilTimes,
    },
    props:{editData:[Object,Array]}
};
</script>

<style scoped>
.card{
    text-align: right;
   
    width: 500px;
}
#card{
    position: fixed;
    top: calc(50% - 300px);
    left: calc(50% - 250px);
}
.close-btn{
    left: 15px;
}
</style>