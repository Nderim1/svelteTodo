<script>
  import { onMount } from "svelte";
  import AddTodo from "./AddTodo/index.svelte";
  import ShowTodos from "./ShowTodos/index.svelte";

  let todoToEdit = "";
  let todoToEditIndex = "";

  let allTodos = [];

  const updateLSTodos = (todos) => {
    localStorage.setItem("todos", JSON.stringify(todos));
  };

  const addTodo = (todo) => {
    allTodos = [].concat(todo, allTodos);
    updateLSTodos(allTodos);
  };

  const removeTodo = (index) => {
    const confirmPopup = window.confirm(
      "Are you sure you want to delete your TODO?"
    );
    if (confirmPopup) {
      allTodos.splice(index, 1);
      // mutate the array so it triggers a rerender
      allTodos = [].concat(allTodos);
      updateLSTodos(allTodos);
    }
  };

  const editTodo = (newText) => {
    allTodos[todoToEditIndex].title = newText;
    allTodos[todoToEditIndex].status = "todo";
    todoToEdit = "";
    todoToEditIndex = "";
  };

  const handleEditTodoClick = (index) => {
    todoToEdit = allTodos[index].title;
    todoToEditIndex = index;
  };

  const handleOnCheckboxCheck = (index, status) => {
    allTodos[index].status = status;
    updateLSTodos(allTodos);
  };

  onMount(() => {
    const LSTodos = localStorage.getItem("todos");
    if (!LSTodos) {
      updateLSTodos(allTodos);
    } else {
      allTodos = JSON.parse(LSTodos);
    }
  });
</script>

<main>
  <h1>My TODO app in Svelte!</h1>
  <p id="description">
    This is a TODO app I build with SvelteJS. <br />
    Check out my other TODO apps I created with other JS frameworks: <br />
    <a href="/" target="_blank" rel="noopener noreferrer">React</a> |
    <a href="/" target="_blank" rel="noopener noreferrer">Vue</a> |
    <a href="/" target="_blank" rel="noopener noreferrer">Solid</a>
  </p>
  <br /><br />
  <AddTodo {addTodo} {todoToEdit} {editTodo} />
  <br />

  <ShowTodos
    {allTodos}
    {handleOnCheckboxCheck}
    {removeTodo}
    editTodo={handleEditTodoClick}
  />
</main>

<style>
  body {
    background-color: #0b7373;
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 400px;
    margin: 0 auto;
  }

  h1 {
    color: #0b7373;
    font-size: 2.5em;
    font-weight: 100;
  }

  #description {
    line-height: 1.8rem;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
