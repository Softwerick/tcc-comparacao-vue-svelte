<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'

  import { onMount } from 'svelte';

  let users = [];

  onMount(async () => {
    const response = await fetch('/data.json');
    const data = await response.json();
    users = data.users;
  });

  function deleteUser(userId) {
    const updatedUsers = users.filter(user => user.id !== userId);
    localStorage.setItem('users', JSON.stringify(updatedUsers));
    users = updatedUsers;
  }

</script>

<main>
  <h1>Lista de usuários</h1>
	<div class="user-grid">
	  {#each users as user}
		<div class="user">
			<p>{user.name} - {user.occupation}</p>
			<img src="/teste.jpg" alt="bla" width="300">
		  <button on:click={() => deleteUser(user.id)}>Deletar</button>
		</div>
	  {/each}
	</div>
</main>

<style>
	.user-grid {
	  display: grid;
	  grid-template-columns: repeat(4, 1fr);
	  gap: 1em;
	}
	.user {
	  background: #f9f9f9;
      color: black;
	  padding: 1em;
	  border-radius: 5px;
	  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}
</style>
