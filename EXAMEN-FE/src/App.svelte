<script>
	import {
		onMount
	} from 'svelte';
	let movies = [];
	let pagination = {};
	onMount(() => {
		getMovies(10, 10).then().catch(e => console.log(e));
	});
	const getMovies = async (take, skip) => {
		URL = `http://localhost:3000/movies/?take=${take}&skip=${skip}`
		// call the api
		const response = await fetch(URL);
		const data = await response.json();
		console.log(data)
		movies = data.data;
		pagination = data.pagination;
		console.log(movies);
		console.log(pagination);
	}
</script>

<main>
	<div class="container">

		<h4 class="mt-10 mb-10">List Movies </h4>
		<table class="table">
			<thead>
				<tr>
					<th scope="col">#</th>
					<th scope="col">Title</th>
					<th scope="col">Genres</th>
					<th scope="col">Year</th>
				</tr>
			</thead>
			<tbody>
				{#each movies as m (m.id)}
				<tr>
					<th scope="row">1</th>
					<td>{m.title}</td>
					<td>{m.genres}</td>
					<td>{m.year}</td>
				</tr>
				{/each}
			</tbody>
		</table>
	</div>
</main>

<style>
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