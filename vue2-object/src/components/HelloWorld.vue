<template>
  <div>
    <input v-model="newItem" @keyup.enter="addItem" placeholder="Add item" />
    <button @click="addItem">新建</button>
    <ListCom :items="items" @remove="remove" @edit="edit"></ListCom>
  </div>
</template>

<script>
import ListCom from './ListCom.vue'
export default {
  components:{
    ListCom
  },
  data() {
    return {
      newItem: "",
      items:[]
    };
  },
  methods: {
    addItem() {
      if (this.newItem.trim()) {
        this.items.push({ text: this.newItem.trim(), isEdit:false,id:Math.random()});
        this.newItem = "";
        console.log(this.items,  64);
      }
    },
    remove(index) {
      this.items.splice(index, 1);
    },
    edit(item,index){
      if(item.isEdit){
        item.isEdit=false;
        this.items[index]=item
      }else{
        item.isEdit=true;
      this.items[index]=item
      }
    }
  },
};
</script>

<style>
/* 样式内容按需添加 */
</style>
