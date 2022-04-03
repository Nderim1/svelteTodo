<script>
  import { onMount } from "svelte";
  export let allTodos;
  export let handleOnCheckboxCheck;
  export let removeTodo;
  export let editTodo;
  import BuildTodo from "./BuildTodo/index.svelte";
</script>

<div id="showTodosContainer">
  <div id="flexContainer">
    {#if allTodos.length}
      {#each allTodos as todo, index}
        {#if todo.title.length}
          <BuildTodo
            key={index}
            todoToDisplay={todo}
            onCheckboxCheck={(status) => handleOnCheckboxCheck(index, status)}
            handleOnEditTodo={() => editTodo(index)}
            removeTodo={() => removeTodo(index)}
          /><br />
        {/if}
      {/each}
    {:else}
      <span>You have no TODOs at the moment!</span>
    {/if}
  </div>
</div>

<style>
  #showTodosContainer {
    display: flex;
    justify-content: center;
  }

  #flexContainer {
    width: 530px;
  }
</style>
