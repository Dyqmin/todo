<script>
	import ToDo from './ToDo.svelte';
	import { fade } from 'svelte/transition';
	let src = "./Vector 1.svg";

	let tasks = JSON.parse(localStorage.getItem("tasks"));
	console.log(tasks);

	const UpdateLocalStorage = () => {
		localStorage.setItem("tasks", JSON.stringify(tasks));
		tasks = JSON.parse(localStorage.getItem("tasks"));
		console.log(`local storage tasks array has been updated. Presenting the array:`);
		console.table(tasks);
	}

	const CheckCurrentLocalStorage = () => {
		console.log(`current local storage array is:`);
		console.table(tasks);
	}
	
	const AddTask = () => {
		tasks.push(document.getElementById("add-task").value);
		console.log(`Task has been added`);
		UpdateLocalStorage();
		document.getElementById("add-task").value = "";
	}

	const deleteTask = (x) => {
		tasks.splice(tasks.indexOf(x),1);
		UpdateLocalStorage();
	}
	
	const HandleKey = (event) => {
		if(event.key=="Enter"){
			AddTask();
		}
	}

</script>

<svelte:window on:keydown={HandleKey}/>

<main>
	<h1>todo</h1>
	<input id="add-task"><button on:click={()=>AddTask()} >add</button>
	<button on:click={()=>CheckCurrentLocalStorage()}>check local storage</button>
	{#each tasks as x}
	<div class="eventListener todo-wrap" on:click={()=>deleteTask(x)}>
	<ToDo task={x}></ToDo>
	</div>
	{/each}
</main>

<style>
@import url('https://rsms.me/inter/inter.css');

	*{
		font-family: 'Inter';

	}
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	.todo-wrap:hover{
		cursor: pointer;
		font-family: "Inter";
		
		/*background: #ff3e00;*/
	}
	.todo-wrap{
		width:30%;
		margin: 0 auto;
		font-size: 16px;
	}
	
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>