<script>
  import Fa from "svelte-fa";
  import { faXmark } from "@fortawesome/free-solid-svg-icons";
  let todos = [];
  let i = 0;

  //Add pressing Enter key to addTodo()
  const handleEnter = (e) => {
    if (e.key === "Enter") {
      addTodo();
    }
  };

  //Add a Todo item to the list of Todos and save it in localStorage
  const addTodo = () => {
    //Handle empty userInput
    if (document.querySelector("input").value === "") {
      console.log("Must enter some text first!");
    } else {
      //Create Todo onject with an id and a task
      var todo = {
        id: i++,
        task: document.querySelector("input").value,
      };
      //Update the global array of todos with the new Todo item
      todos = [...todos, todo];
      //Save the global array of todos to localStorage
      localStorage.setItem("todoApp", JSON.stringify(todos));
      //Clear and focus on the todo input box
      document.querySelector("input").value = "";
      document.querySelector("input").focus();
    }
  };

  //Remove a Todo from the list
  const deleteTodo = (e) => {
    //Remove specific item from global array of todos by id
    todos = todos.filter(
      (item) => item.id !== Number(e.target.parentElement.id)
    );
    //Update localStorage
    localStorage.setItem("todoApp", JSON.stringify(todos));
  };

  const loadTodos = () => {
    //check for todos in local storage
    var data = localStorage.getItem("todoApp");
    //If there is no previous data
    if (!data) {
      todos = [];
    } else {
      //Set global array of todos to whatever was read from localStorage
      todos = JSON.parse(data);
      //Update index TODO: find a better way to do this
      i = todos.length;
    }
  };

  loadTodos();
</script>

<!-- Add eventListener to window -->
<svelte:window on:keyup={handleEnter} />

<main>
  <label for="todo-input">Todo: </label>
  <input type="text" name="todo-input" />
  <button on:click={addTodo}> Add Todo </button>
  <ul>
    {#each todos as todo}
      <li id={todo.id}>
        {todo.task}
        <button on:click={deleteTodo}>
          <!-- <Fa icon={faXmark} /> -->
          X
        </button>
      </li>
    {/each}
  </ul>
</main>

<style>
  input {
    background-color: magenta;
    border: none;
    border-radius: 5px;
    height: 35px;
  }
  ul {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  li {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 300px;
    height: 50px;
    border-radius: 10px;
    margin: 8px 0;
    padding: 0 10px;
    background-color: navy;
  }

</style>
