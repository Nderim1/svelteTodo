<script>
  import { beforeUpdate, afterUpdate } from "svelte";
  export let addTodo;
  export let todoToEdit;
  export let editTodo;
  $: todoToAdd = todoToEdit || "";

  const prepareAndAddTodo = (todo) => {
    if (todo.length) {
      const otherTodoProps = {
        title: todo,
        status: "todo",
        description: "",
      };
      addTodo(otherTodoProps);
    }
  };

  const handleAddTodoClick = () => {
    prepareAndAddTodo(todoToAdd);
    todoToAdd = "";
  };

  const handleAddTodoEnter = (event) => {
    if (event.code === "Enter") {
      if (todoToEdit) {
        handleEditTodoClick();
      } else {
        prepareAndAddTodo(todoToAdd);
        todoToAdd = "";
      }
    }
  };

  const handleEditTodoClick = () => {
    if (todoToAdd) {
      editTodo(todoToAdd);
    }
    todoToAdd = "";
    todoToEdit = "";
  };
</script>

<div id="addTodoContainer">
  <input
    placeholder="Enter your TODO"
    bind:value={todoToAdd}
    on:keypress={handleAddTodoEnter}
    maxlength="50"
  />
  <button
    id="addTodoBtn"
    class="glow-on-hover"
    on:click={() => {
      todoToEdit ? handleEditTodoClick() : handleAddTodoClick();
    }}>{todoToEdit ? "Edit TODO" : "Add TODO"}</button
  >
</div>

<style>
  input {
    max-width: 355px;
    width: 40%;
    border-radius: 10px 0px 0px 10px;
    background-color: floralwhite;
    outline: none;
    border: 2px solid black;
    height: 40px;
    color: #0b7373;
  }

  ::placeholder {
    color: #0b73738e;
  }

  .glow-on-hover {
    border: 2px solid black;
    height: 40px;
    width: 120px;
    outline: none;
    color: #0b7373;
    background-color: floralwhite;
    cursor: pointer;
    position: relative;
    z-index: 0;
    border-radius: 0px 10px 10px 0px;
  }

  .glow-on-hover:before {
    content: "";
    background: linear-gradient(
      45deg,
      #ff0000,
      #ff7300,
      #fffb00,
      #48ff00,
      #00ffd5,
      #002bff,
      #7a00ff,
      #ff00c8,
      #ff0000
    );
    position: absolute;
    top: -2px;
    left: -2px;
    background-size: 400%;
    z-index: -1;
    filter: blur(5px);
    width: calc(100% + 4px);
    height: calc(100% + 4px);
    animation: glowing 20s linear infinite;
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
    border-radius: 0px 10px 10px 0px;
  }

  .glow-on-hover:active {
    color: #000;
  }

  .glow-on-hover:active:after {
    background: transparent;
  }

  .glow-on-hover:hover:before {
    opacity: 1;
  }

  .glow-on-hover:after {
    z-index: -1;
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: floralwhite;
    left: 0;
    top: 0;
    border-radius: 0px 10px 10px 0px;
  }

  @keyframes glowing {
    0% {
      background-position: 0 0;
    }
    50% {
      background-position: 400% 0;
    }
    100% {
      background-position: 0 0;
    }
  }
</style>
