<template>
  <div class="main">
    <div class="wrapper">
      <div class="grid-containers">
        <div class="grid-containers__container">
          <PopupContainer 
            position="left" 
            :title="titleCount(shoppingList, 'SHOPPING LIST ')" 
            id="popup_1"
            @closeContainer="closeContainer"
          > 
            <TodoList :listArray="shoppingList" @event="toggleItemShopping" />
          </PopupContainer>
          <OpenPopup 
            position="left" 
            :title="titleCount(shoppingList, 'SHOPPING LIST ')" 
            idOpenContainer="popup_1"
            @openContainer="openContainer"
          />
        </div>
        <div class="grid-containers__container">
          <LikedContainer @closeContainer="closeContainer" id="popup_2"/>
          <OpenPopup 
            position="right" 
            title="KITTY" 
            idOpenContainer="popup_2"
            @openContainer="openContainer"
          />
        </div>
        <div class="grid-containers__container">
          <PopupContainer 
            position="left" 
            title="MAMAAA OOOO" 
            id="popup_3"
            @closeContainer="closeContainer"
          >
            <Text3 :color="TEXT_COLORS.DARK">THIS ONE IS NOT A LIST - JUST SOME PLAIN OL’ TEXT.</Text3>            
            <br><br>
            <Text3 :color="TEXT_COLORS.DARK">IS THIS THE REAL LIFE </Text3>
            <Text3 :color="TEXT_COLORS.DARK">IS THIS JUST FANTASY</Text3>
            <Text3 :color="TEXT_COLORS.DARK">CAUGHT IN A LANDSIDE</Text3>
            <Text3 :color="TEXT_COLORS.DARK">NO ESCAPE FROM REALITY</Text3>
            <br><br>
            <Text3 :color="TEXT_COLORS.DARK">
              BY THE WAY IF THERE WAS A REALLY LONG LINE, I’M PRETTY SURE AT SOME POINT IT WOULD WRAP TO THE NEXT LINE. JUST LIKE THE OTHER ELEMENTS ON THIS PAGE, THIS ONE HAS A PRE-DEFINED MAX-WIDTH 
            </Text3>            
          </PopupContainer>
          <OpenPopup 
            position="left" 
            title="MAMAAA OOOO" 
            idOpenContainer="popup_3"
            @openContainer="openContainer"
          />
        </div>
        <div class="grid-containers__container">
          <PopupContainer 
            position="right" 
            :title="titleCount(booksToRead, 'BOOKS TO READ ')" 
            id="popup_4"
            @closeContainer="closeContainer"
          >
            <TodoList :listArray="booksToRead" @event="toggleItemBooks" />
          </PopupContainer>
          <OpenPopup 
            position="right" 
            :title="titleCount(booksToRead, 'BOOKS TO READ ')" 
            idOpenContainer="popup_4"
            @openContainer="openContainer"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
  import PopupContainer from '@/components/PopupContainer.vue'
  import OpenPopup from '@/components/OpenPopup.vue'
  import LikedContainer from '@/components/LikedContainer.vue'
  import TodoList from '@/components/TodoList.vue'
  import Text3 from '@/components/Typograpy/Text3.vue'
  import { TEXT_COLORS } from './components/Typograpy/constants'

  export default {
    components: {
      PopupContainer, OpenPopup, LikedContainer, TodoList, Text3
    },
    data() {
      return {
        TEXT_COLORS: TEXT_COLORS,
        shoppingList: [
          { name: 'MILK' },
          { name: 'BREAD' },
          { name: 'HAM' },
          { name: 'CHEESE' },
          { name: 'WATER' },
        ],
        booksToRead: [
          { name: 'SAPIENS BY YUVAL NOAH HARARI' },
          { name: 'THE THEORY OF EVERYTHING BY STEPHEN HAWKING' },
          { name: 'A WILD SHEEP CHASE BY HARUKI MURAKAMI' },
          { name: 'CLEAN CODE BY ROBERT MARTIN' },
        ]
      }
    },
    mounted() {
      this.shoppingList = this.shoppingList.map( function( item:any) {
        return {
          ...item,
          id: Math.random(),
          isCompleted: false
        }
      }) 
      this.booksToRead = this.booksToRead.map( function( item:any) {
        return {
          ...item,
          id: Math.random(),
          isCompleted: false
        }
      }) 
    },
    methods: {
      toggleItemShopping(id: number) {
        this.shoppingList = this.toggleItemInTodoList(this.shoppingList, id);        
      },
      toggleItemBooks(id: number) {
        this.booksToRead = this.toggleItemInTodoList(this.booksToRead, id);  
      },
      toggleItemInTodoList(array: any, id: number) {
        return array.map( function (item:any) {
          return {
            ...item,
            isCompleted: 
              item.isCompleted && item.id === id 
              ? false 
              : item.id === id 
                ? true 
                : item.isCompleted
          }
        })        
      },
      titleCount(arr: any, firstText: string) {
        let count = 0;
        arr.map( function( item:any ) {
          if(item.isCompleted) {
            count++
          }
        })     
        return firstText + '[' + count + '/' + arr.length + ']'
      },
      closeContainer(position: any, id: string, toOpen: string) {
        let popup = document.getElementById(id)
        let openPopup = document.getElementById(`openPopup-${id}`);
        
        let widthPopup = popup!.offsetWidth + 45;
        let toScroll = 0
        let toClose = 0
        let startPosition = Number(openPopup!.style[position].substring(0, openPopup!.style[position].length - 2))
        
        if(position === 'left' || position === 'right') {
          setInterval(function() {
            if (widthPopup <= 0) {
              clearInterval()
            } else {
              widthPopup = widthPopup - 3;
              toScroll = !toOpen ? toScroll + 300 : toScroll + 3 
              popup!.style[position] = '-' + toScroll + 'px'
            }            
          }, 1);
          if(toOpen) {
            setInterval(function() {
              if (toClose >= 60) {
                clearInterval()
              } else {
                toClose = toClose + 3
                openPopup!.style[position] = (startPosition + toClose) + 'px'
              }            
            }, 1);
          }
        } 
      },
      openContainer(position: any, id: string) {
        let popup = document.getElementById(id)
        let openPopup = document.getElementById(`openPopup-${id}`);

        let widthPopup = popup!.offsetWidth + 45;
        let toScroll = -widthPopup
        let toClose = 0
        let startPosition = Number(openPopup!.style[position].substring(0, openPopup!.style[position].length - 2))
        
        if(position === 'left' || position === 'right') {
          setInterval(function() {
            if (toClose >= 60) {
              clearInterval()
            } else {
              toClose = toClose + 3
              openPopup!.style[position] = (startPosition - toClose) + 'px'
            }            
          }, 1);
          setInterval(function() {
            if (toScroll >= widthPopup) {
              clearInterval()
            } else {
              widthPopup = widthPopup - 3;
              toScroll = toScroll + 3
              popup!.style[position] = toScroll + 'px'
            }            
          }, 1);
        } 
      },
    }
  }
</script>

<style scoped lang="scss">
.main {
  background: $dark;
  width: 100%;
  height: 100vh;
  font-size: 20px;
  font-family: sans-serif;
  text-transform: uppercase;
  overflow-x: hidden;
}
.grid-containers {
  display: grid;
  width: 100vw;
  height: 100vh;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  position: relative;
  &__container {
    position: relative;
    &:nth-child(2n) {
      .popupContainer {
        right: 0;
        left: auto;
      }
    }
  }
  .popupContainer {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);    
  }
}
.flex-column {
  display: flex;
  flex-direction: column;
}
</style>
