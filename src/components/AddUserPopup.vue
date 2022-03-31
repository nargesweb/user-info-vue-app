<template>
    <div class="d-flex align-item-center justify-content-center translate-middle shadow-lg" id="card" >
        <form class ="card p-4 rounded-3" onSubmit="return false">
            <div class="mb-5">
                <button class="position-absolute close-btn btn btn-outline-secondary rounded-circle p-1 d-flex align-item-center justify-content-center mb-3"  @click="openingAddItem"><UilTimes /></button>
            </div>
            <h3 class="mb-4">فرم زیر را پر کنید</h3>
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
            <button type="submit" class="btn btn-primary" @click="sendUserData">Submit</button>
            
        </form>
    </div>
</template>

<script>
import eventBus from "../services/eventBus.js"
// icon 
import { UilTimes } from '@iconscout/vue-unicons'
export default {
    name: 'add-user-popup',

    data() {
        return {
            name:"",
            family:"",
            code:"",
            city:"",
        };
    },
    components:{
        UilTimes
    }
    ,
    methods: {
        openingAddItem(){
            eventBus.$emit("openAddItem")
        },
        sendUserData(){
            if(this.name == "" || this.family == "" ||this.code == "" || this.city == ""){
                alert("جدول را کامل کنید ")
            }else{
                eventBus.$emit("addUser",{name:this.name,family :this.family,code :this.code,city :this.city});
                this.name = ""
                this.family = ""
                this.code = ""
                this.city = ""
                this.openingAddItem();
            }
        }
    },
    props:{
       
    }
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