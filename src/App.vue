<template>
  <div class="container">
    <div class="content">
      <header class="header">
        <h1 class="title">ToDo App</h1>
      </header>
      <form class="form">
        <label class="form__label">
          <span>Task:</span>
          <input
          v-model="newTask"
          type="text"
          placeholder="What do you need to do?"
          class="form__input">
        </label>
        <button @click.prevent="add" class="form__btn btn btn--add">Add</button>
      </form>
      <button @click="clear" class="btn btn--clear">Clear list</button>
      <transition-group tag="ol" name="fade" class="list">
        <li v-for="(task, index) in tasks" :key="index" class="list__item item">
          <span class="item__title">Task {{ index + 1 }}:</span>
          <span class="item__disription">{{ task }}</span>
          <button @click="remove(index)" :key="task" class="btn btn--remove">x</button>
        </li>
      </transition-group>
    </div>
    <footer class="footer">
      TO DO © 2018 Weronika Kędziora
    </footer>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tasks: ['Learn Vue.js', 'Another random task'],
      newTask: ''
    }
  },
  methods: {
    // add new task
    add () {
      if (this.newTask.length > 0) {
        this.tasks.push(this.newTask)
        this.newTask = ''
      }
    },
    // remove chosen task
    remove (index) {
      this.tasks.splice(index, 1)
    },
    // clear all tasks
    clear () {
      this.tasks = []
    }
  }
}
</script>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    color: #fff;
    font-family: 'Arima Madurai', serif;
    font-size: 18px;
  }

  body{
    background-color: #192d42;
  }

  .container{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 100vh;
  }

   .content{
     display: flex;
     flex-direction: column;
     justify-content: center;
     align-items: center;
   }

  .title{
    font-size: 15vh;
    padding: 10px;
    margin: 10px;
    text-align: center;
  }

  .form{
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px;
    &__input{
      padding: 8px;
      margin: 4px 10px;
      border-radius: 10px;
      color: #192d42;
      background-color: #fff;
      border: 4px solid #192d42;
      }
  }

  .btn{
    margin: 10px;
    padding: 5px 10px;
    border-radius: 15px;
    cursor: pointer;
    border: 2px solid #fff;
    background-color: #081c31;
    transition: background-color 0.2s;
    &--add:hover{
      background-color: #009b0c
    }
    &--clear:hover{
      background-color: #111;
    }
    &--remove{
      margin: 0 0 0 5px;
      border-width: 0;
      padding: 2px 10px;
      border-radius: 5px;
      background-color: #192d42;
      &:hover{
        background-color: #9b0000;
      }
    }
  }

  .list{
    margin-top: 40px;
    &__item{
      margin: 6px 20px;
      padding-left: 10px;
      display: flex;
      align-items: center;
    }
  }

  .item__disription{
    flex: 1;
    padding: 5px 10px;
    margin: 6px 0px 6px 20px;
    white-space: normal;
    background-color: #3b4f64;
    border: 1px solid #f8f8f8;
    border-radius: 10px;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .footer{
    color: #222;
    background-color: #fff;
    padding: 10px;
    text-align: center;
    width: 100%;
    font-size: 20px;
    margin-top: 20px;
  }


  @media (max-width: 500px){
    .title{
      font-size: 50px;
    }
    .btn{
      margin: 5px;
      font-size: 20px;
      &--add{
        background-color: #009b0c;
        margin-top: 20px;
        width: 50vw;
      }
      &--clear{
        background-color: #222;
        width: 50vw;
      }
    }
    .footer, .item__disription {
      font-size: 15px;
    }
    .form{
      flex-direction: column;
      &__label{
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
      }
      &__input{
        width: 90vw;
        overflow: hidden;
      }
    }
  }


</style>
