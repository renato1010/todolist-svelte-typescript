<script lang="ts" context="module">
  import type { TodoProp } from "./Todo.svelte";
</script>

<script lang="ts">
  import Todo from "./Todo.svelte";

  let lastId = 0;
  const createTodo = (text: string, done: boolean = false): TodoProp => ({ id: ++lastId, text, done });
  let todoText = "";
  let todos: TodoProp[] = [createTodo("learn Svelte", true), createTodo("build a Svelte app")];
  $: uncompletedCount = todos.filter((t) => !t.done).length;
  $: status = `${uncompletedCount} of ${todos.length} remaining`;
  const addTodo = () => {
    todos = [...todos, createTodo(todoText)];
    todoText = "";
  };
  const archiveCompleted = () => {
    todos = todos.filter((t) => !t.done);
  };
  const deleteTodo = (todoId: number) => {
    todos = todos.filter((t) => t.id !== todoId);
  };
  const toggleDone = (todo: TodoProp) => {
    const { id } = todo;
    todos = todos.map((t) => (t.id === id ? { ...t, done: !t.done } : t));
  };
</script>

<div>
  <h1>To Do List</h1>
  <div>
    {status}
    <button on:click={archiveCompleted}>Archive Completed</button>
  </div>
  <form on:submit|preventDefault>
    <input size="30" placeholder="enter new todo" bind:value={todoText} />
    <button disabled={!todoText} on:click={addTodo}>Add</button>
  </form>
  <ul>
    {#each todos as todo}
      <Todo {todo} on:delete={() => deleteTodo(todo.id)} on:toggleDone={() => toggleDone(todo)} />
    {/each}
  </ul>
</div>

<style>
  button {
    margin-left: 10px;
  }
  ul {
    list-style: none; /* removes bullets */
    margin-left: 0;
    padding-left: 0;
  }
</style>
