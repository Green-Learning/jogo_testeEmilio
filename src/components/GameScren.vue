<template>

  <div class="game-screen ">
    <div class="score">Score: {{ score }}</div>

    <TrashBin binType="recyclable" ref="recyclableBin"/>
    <TrashBin binType="organic" ref="organicBin"/>
    
    <TrashItem
      v-for="(item, index) in items"
      :key="index"
      :itemType="item.type"
      :binTypes="item.binTypes"
      @itemDropped="handleItemDropped"
    />
  </div>

</template>

<script>
import TrashBin from "@/components/TrashBin.vue";
import TrashItem from "@/components/TrashItem.vue";

export default {
  components: {
    TrashBin,
    TrashItem,
  },
  data() {
    return {
      items: [
        { type: "bottle", binTypes: ["recyclable"] },
        { type: "plastic", binTypes: ["recyclable"] },
        { type: "cup", binTypes: ["recyclable"] },
        { type: "pizza", binTypes: ["organic"] },
        { type: "cookie", binTypes: ["organic"] },
        { type: "burger", binTypes: ["organic"] },
      ],
      score: 0,
    };
  },
  methods: {
    handleItemDropped(binType) {
      const item = this.items.find(item => item.binTypes.includes(binType));
      
        console.log(item.binTypes);
        console.log(binType);
        console.log

        if (item.binTypes.includes(binType)) {
          this.score += 10;
          console.log(`Item dropped in the correct bin (${binType}). Score: ${this.score}`);
        } else if(item.binTypes.indexOf(binType) === -1){
          console.log(`Item dropped in the wrong bin (${binType}). Score: ${this.score}`);
        }      
    },

    handleBinAction(binType, itemType){
      if (binType === 'recyclable') {
        // Lógica específica para a lixeira recyclable
        this.recyclableBinAction(itemType);
      } else if (binType === 'organic') {
        // Lógica específica para a lixeira organic
        this.organicBinAction(itemType);
      }
    },
    recyclableBinAction(itemType) {
      // Lógica para a lixeira recyclable
      console.log(`Recyclable bin action for item type: ${itemType}`);
      // Faça o que for necessário para este caso
    },
    organicBinAction(itemType) {
      // Lógica para a lixeira organic
      console.log(`Organic bin action for item type: ${itemType}`);
      // Faça o que for necessário para este caso
    },

  },
};
</script>

<style scoped>
.game-screen {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

.score {
  font-size: 24px;
  margin-bottom: 20px;
}
</style>
