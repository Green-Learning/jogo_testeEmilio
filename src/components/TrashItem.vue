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
      binTypes: Array, // Recebe os tipos de lixeira onde o item pode ser colocado
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
  
        // Verificar colisão com as lixeiras
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
            // Item colocado na lixeira correta!
            this.$emit('itemDropped', this.itemType);
            break; // Encerra o loop após encontrar a lixeira correta
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
  
  .bottle {
    background-color: #4caf50;
    /* Estilo da garrafa */
  }
  
  .plastic {
    background-color: #4caf50;
    /* Estilo do plástico */
  }
  
  .cup {
    background-color: #4caf50;
    /* Estilo do copo */
  }
  
  .pizza {
    background-color: #ff9800;
    /* Estilo da pizza */
  }
  
  .cookie {
    background-color: #ff9800;
    /* Estilo do biscoito */
  }
  
  .burger {
    background-color: #ff9800;
    /* Estilo do hambúrguer */
  }
  </style>