<template>
  <div>
    <ul>
      <li v-for="(item, index) in items" :key="item.id">
        <div>第 {{ change(index + 1) }}条</div>
        <input v-show="item.isEdit" v-model="item.text" />
        <span v-show="!item.isEdit"> {{ item.text }}</span>
        <div>
          <button @click="removeItem(index)">删除</button>
          <button @click="edit(item,index)">{{ item.isEdit?'保持' : '修改' }}</button>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
   
    }
  },
  props:{
    items:{

    }
  },
  mounted(){


  },
  computed:{
 
  },
  methods:{
    change(value) {
      const chineseNumbers = ["", "一", "二", "三", "四", "五", "六", "七", "八", "九"];
      const chineseUnits = ["", "十", "百", "千", "万", "亿"];

      if (value === 0) {
        return chineseNumbers[0];
      }

      let result = "";
      let unitIndex = 0;

      const valueOle = value;

      while (value > 0) {
        const digit = value % 10;
        if (digit !== 0 || unitIndex === 1) {
          result = chineseNumbers[digit] + chineseUnits[unitIndex] + result;
        }
        value = Math.floor(value / 10);
        unitIndex++;
      }

      if (valueOle > 9 && valueOle < 20) {
        // 把10：十一，处理为：十
        result = result.slice(1);
        console.log("111", result.slice(1));
      }

      return result;
    },
    removeItem(index) {
      this.$emit('remove',index)
      // this.items.splice(index, 1);
    },
    edit(item,index){
      this.$emit('edit',item,index)
    }
  },
}
</script>
<style scoped>

</style>./List.vue
