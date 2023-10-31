<template>
    <div
      class="trash-item"
      :class="itemType"
      :style="{ left: position.x + 'px', top: position.y + 'px' }"
      @mousedown="startDragging"
      @mousemove="drag"
      @mouseup="stopDragging"
    ></div>
  </template>
  
  <script>
  export default {
    props: {
      itemType: String,
      binTypes: Array,
    },
    data() {
      return {
        isDragging: false,
        position: { x: 0, y: 0 },
        offset: { x: 0, y: 0 },
      };
    },
    methods: {
      startDragging(event) {
        this.isDragging = true;
        this.offset.x = event.clientX - this.position.x;
        this.offset.y = event.clientY - this.position.y;
      },
      drag(event) {
        if (this.isDragging) {
          this.position.x = event.clientX - this.offset.x;
          this.position.y = event.clientY - this.offset.y;
        }
      },
      stopDragging() {
        this.isDragging = false;
  
        const trashItemRect = this.$el.getBoundingClientRect();
        for (const binType of this.binTypes) {
            
          const bin = document.querySelector(`.trash-bin.${binType}`);
          const binRect = bin.getBoundingClientRect();

          if (
            trashItemRect.left >= binRect.left &&
            trashItemRect.right <= binRect.right && 
            trashItemRect.top >= binRect.top &&
            trashItemRect.bottom <= binRect.bottom
          ) {
            this.$emit('itemDropped', binType);
            return; // Encerra a verificação após encontrar a lixeira correta
          }
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .trash-item {
    position: absolute;
    width: 50px;
    height: 50px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    cursor: grab;
  }
  
  /* Estilos para diferentes tipos de itens */
  .bottle {
    background-color: #4caf50;
  }
  
  .plastic {
    background-color: #4caf50;
  }
  
  .cup {
    background-color: #4caf50;
  }
  
  .pizza {
    background-color: #ff9800;
  }
  
  .cookie {
    background-color: #ff9800;
  }
  
  .burger {
    background-color: #ff9800;
  }
  </style>
  