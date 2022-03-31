<template>
  <div id="App" class="bg-light mt-4">
    <div class="container-xl bg-white border p-0 shadow-sm ">
      <Header />
      <div class="form-floating w-100  mt-5 container-xl d-flex ">
        <input type="text" class="form-control shadow-sm rounded-pill p-3" placeholder="جستجو ..." v-model="search" >
      </div>
      <Table :filtered="filtered" class="p-4" />
      <AddUserPopup v-if="openAddPopup"  />
      <EditUsersItem :editData="editData" v-if="openEditPopup"  />
    </div>
  </div>
</template>

<script>
// components 
import Header from "./components/Header.vue"
import Table from "./components/Table.vue"
import AddUserPopup from "./components/AddUserPopup.vue"
import EditUsersItem from "./components/EditUsersItem.vue"
// eventBus 
import eventBus from "./services/eventBus.js"

export default {
  name: 'App',
  components: {
   Table,Header,AddUserPopup,EditUsersItem
  },
  data(){
    return{
      search:"",
      openAddPopup : false,
      openEditPopup : false,
      edit : false,
      editData : [],
      index:'',
      addUser:false,
      // fake users
      users:[
        {id:1,name:"علی",family:"پورصمدی",code:"12345",city:"تهران"},
        {id:2,name:"محمد",family:"فرشتیان",code:"34521",city:"کرج"},
        {id:3,name:"علی اصغر",family:"ده نمکی",code:"78945",city:"بابل"},
        {id:4,name:"رستم",family:"خالقی",code:"96541",city:"ساری"},
        {id:5,name:"امید",family:"رضازاده",code:"36985",city:"اصفهان"},
        {id:6,name:"سیامک",family:"انصاری",code:"41785",city:"کاشان"},
        {id:7,name:"شهاب",family:"رضایی",code:"69853",city:"شیراز"},
      ]
    }
  },
  // search filter
  computed: {
    filtered(){
      return this.users.filter(user => {
          return user.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  },
  methods:{
    // open and colse addUsers and  Edit popup 
    openAddUserPopup(){
      return !this.openAddPopup ? this.openAddPopup = true : this.openAddPopup = false
    },
    openEditUserPopup(){
      return this.openEditPopup ? this.openEditPopup = false : this.openEditPopup = true;
    },
    // add users in table
    addUserItems (data){
      this.users.push(data)
    },
    // edit users in table
    EditUserItems (data){
      this.users[this.index].name = data.name
      this.users[this.index].family = data.family
      this.users[this.index].city = data.city
      this.users[this.index].code = data.code
    },
    // remove users on table
    removeUserItem(index){
      this.users.splice(index,1)
    },
    // find index to show users Info in Edit table
    findUser(index){
      this.index = index
      let findIndex = this.users.filter((user,userIndex) => userIndex == this.index )
      this.editData = findIndex[0]; 
      this.openEditPopup = true
    }
  },
  created(){
    eventBus.$on("openAddItem",()=>{
      this.openAddUserPopup()
    }),
    eventBus.$on("openEdit",()=>{
      this.openEditUserPopup()
    }),
    eventBus.$on("addUser",data=>{
      this.addUserItems(data)
    }),
    eventBus.$on("editingUser",data=>{
      this.EditUserItems(data)
    }),
    eventBus.$on("removeUser", index =>{
      this.removeUserItem(index)
    }),
    eventBus.$on("editUser" , index =>{
      this.findUser(index)
    })
  }
}
</script>

<style>

html{
  background-color: #f8f9fa;
}


</style>
