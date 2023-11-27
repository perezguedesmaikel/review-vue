<script lang="ts" setup>
import {reactive, ref, Ref} from "vue";
import NewInput from "../components/canvas-component/NewInput.vue";
//probe
const draggingItem = ref<IItems | null>(null);
let draggingBoard = reactive([]);
let initBoard = reactive<IBoard>({} as IBoard)

interface IItems {
  id: string,
  title: string
}

interface IBoard {
  items: IItems[]
}

//probe git
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
  if (name !== '') {
    boards.push({
      id: crypto.randomUUID(),
      name: name!, items: [],

    })
  }

}

function starDrag(item: any, board: any) {
  console.log('Aquí se empieza a arrastrar', item)
  draggingItem.value = item
  draggingBoard = board
}

function drop(board: any) {
  console.log('Aquí se soltó', board)
  board.items.push(draggingItem.value)
  //drop
  const itemsTemp: IItems[] = initBoard.items
  initBoard.items = itemsTemp.filter(el => el.id !== draggingItem.value!.id!)
}


function dragStart(board: any) {
  console.log('Aquí comienzo', board)
  initBoard = board
}
</script>

<template>
  <v-container class="ContainerStyle">
    <v-label>Canvas Table</v-label>
    <nav>
      <v-btn class="StyleCreateBoard" href="#" @click="createBoard">Create board</v-btn>
    </nav>
    <div class="board-container">
      <div class="Boards">
        <div v-for="board in boards" :key="board.id" :draggable="true" class="Board" @dragstart="()=>dragStart(board)"
             @drop="()=>drop(board)" @dragover.prevent @dragenter.prevent>
          <div>{{ board.name }}</div>
          <NewInput @on-new-items="(text)=>handleEmitNewInput(text,board)"/>
          <div class="items">
            <div v-for="item in board.items" :key="item.id" :draggable="true" class="item"
                 @dragstart="()=>starDrag(item,board)" @dragover.prevent @dragenter.prevent>
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

.StyleCreateBoard {
  margin-bottom: 10px;
  text-decoration: none;
  font-size: large;
  color: blueviolet;
}
</style>
