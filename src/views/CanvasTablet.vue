<script lang="ts" setup>
import {reactive, Ref} from "vue";
import NewInput from "../components/canvas-component/NewInput.vue";

let boards = reactive([
  {
    id: crypto.randomUUID(),
    name: 'Tablero 1', items: [
      {
        id: crypto.randomUUID(),
        title: 'Feature de archivos',
      },
      {
        id: crypto.randomUUID(),
        title: 'Resolver bug',
      }
    ],
  },
  {
    id: crypto.randomUUID(),
    name: 'Tablero 2', items: [
      {
        id: crypto.randomUUID(),
        title: 'Mandar reporte',
      },
      {
        id: crypto.randomUUID(),
        title: 'Code review',
      }
    ],
  }
])

function handleEmitNewInput(text: Ref<string>, board: any) {
  board.items.push({
    id: crypto.randomUUID(),
    title: text.value
  })
}

function createBoard() {
  const name = prompt('Name of the board')
  boards.push({
    id: crypto.randomUUID(),
    name: name, items: [],

  })
}
</script>

<template>
  <v-container class="ContainerStyle">
    <v-label>Canvas Table</v-label>
    <nav>
      <ul>
        <li>
          <a href="#" @click="createBoard">Create board</a>
        </li>
      </ul>
    </nav>
    <div class="board-container">
      <div class="Boards">
        <div v-for="board in boards" :key="board.id" class="Board">
          <div>{{ board.name }}</div>
          <NewInput @on-new-items="(text)=>handleEmitNewInput(text,board)"/>
          <div class="items">
            <div v-for="item in board.items" :key="item.id" class="item">
              {{ item.title }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </v-container>

</template>

<style scoped>
.ContainerStyle {
  padding: 50px;
  opacity: 100%;
}

.Boards {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.Board {
  width: 200px;
  background: #efefef;
  padding: 10px;
}

.items {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.item {
  background-color: white;
  padding: 10px;
  box-sizing: border-box;
}
</style>
