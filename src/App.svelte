<script>
  import ToDo from "./ToDo.svelte";
  let src = "./Vector 1.svg";

  let uid = 1;

  let tasks = [
    {
	  uid: uid++,
	  complete: false,
      description: "test"
    },
    {
	  uid: uid++,
	  complete: false,
      description: "test 2"
    }
  ];

  function addTask (input) {
    const task = {
	  uid: uid++,
	  complete: false,
      description: input.value
    };
    tasks = [task, ...tasks];
    input.value = "";
  };

  function removeTask(event) {
	const { uid } = event.detail;
	tasks = tasks.filter(e => e.uid !== uid);
  }

  function updateStatus(event) {
	const { uid, newStatus } = event.detail;
	tasks = tasks.map(e => e.uid === uid ? {...e, complete: newStatus} : e);
  }
</script>

<main>
  <h1>todo</h1>
  <input
    placeholder="what needs to be done?"
    on:keydown={e => e.which === 13 && addTask(e.target)} />

  {#each tasks as task (task.uid)}
      <ToDo {...task} on:remove={removeTask} on:toggle={updateStatus}></ToDo>
  {/each}
</main>

<style>
  @import url("https://rsms.me/inter/inter.css");

  * {
    font-family: "Inter";
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
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

