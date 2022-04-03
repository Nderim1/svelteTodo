<script>
  export let todoToDisplay;
  export let onCheckboxCheck;
  export let key;
  export let handleOnEditTodo;
  export let removeTodo;

  import FaPencilAlt from "svelte-icons/fa/FaPencilAlt.svelte";
  import FaTrashAlt from "svelte-icons/fa/FaTrashAlt.svelte";
  import FaCheck from "svelte-icons/fa/FaCheck.svelte";

  let test = "hello there";
  let editMode = false;
  const today = new Date();
  let isTodoDone = todoToDisplay.status === "done";
  let dateAndTime = today.toLocaleString();

  const onFakeCheckboxClick = () => {
    isTodoDone = todoToDisplay.status !== "done";
    let status = isTodoDone ? "done" : "todo";
    onCheckboxCheck(status);
    updateTimeAndDate();
    isTodoDone = false;
  };

  const updateTimeAndDate = () => {
    dateAndTime = new Date().toLocaleString();
  };
</script>

<div id="buildTodoContainer">
  <div id="myCustomCheckbox" on:click={onFakeCheckboxClick}>
    {#if todoToDisplay.status === "done"}
      <div><FaCheck /></div>
    {/if}
  </div>
  <!-- <span id="dateAndTime">{dateAndTime}</span> -->
  <!-- {#if editMode}
    <input id="editInput" bind:value={todoToDisplay.title} />
    {/if}
    {:else} -->
  <span
    id="todoTitle"
    class={todoToDisplay.status}
    on:click={() => (editMode = true)}>{todoToDisplay.title}</span
  >
  <div class="actionContainer">
    <div class="actionIcons" on:click={handleOnEditTodo}>
      <FaPencilAlt />
    </div>
    <div class="actionIcons" on:click={removeTodo}>
      <FaTrashAlt />
    </div>
  </div>
</div>

<style>
  #buildTodoContainer {
    display: flex;
    background-color: #282626;
    padding: 10px;
    border-radius: 10px;
  }

  #myCustomCheckbox {
    height: 20px;
    width: 20px;
    min-width: 20px;
    background-color: antiquewhite;
    margin-right: 15px;
    cursor: pointer;
    color: #0b7373;
  }

  .done {
    text-decoration: line-through;
  }

  #dateAndTime {
    margin-right: 10px;
    font-size: 12px;
  }

  #todoTitle {
    cursor: pointer;
  }

  #editInput {
    margin: 0;
    height: 40px;
    border-radius: 10px;
    background-color: floralwhite;
    outline: none;
    border: 2px solid black;
    color: #0b7373;
    font-size: 12px;
    margin: -10px -10px -10px 0px;
  }

  .actionIcons {
    height: 20px;
    width: 20px;
    cursor: pointer;
    margin-left: 10px;
  }

  .actionContainer {
    margin-left: auto;
    display: inline-flex;
  }
</style>
