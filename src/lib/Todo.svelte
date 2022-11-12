<script>
  let todos = []
  window.addEventListener('keyup', function (e) {
    if(e.key === 'Enter') {
      addTodo()
    }
  })
  const addTodo = () => {
    todos = [...todos, document.querySelector('input').value]
    document.querySelector('input').value = ''
  }
</script>

<main>
  <label for="todo-input">Todo: </label>
  <input type="text" name="todo-input">
  <button on:click={addTodo}>
    Add Todo
  </button>
  <ul>
    {#each todos as todo}
      <li>{todo}</li>
    {/each}
  </ul>
</main>

<style>

  ul {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  li {
    display: flex;
    flex-direction: row;
    justify-content: left;
    align-items: center;
    width: 300px;
    height: 50px;
    border-radius: 10px;
    margin: 8px 0;
    padding: 0 10px;
    background-color: navy;
  }
</style>
