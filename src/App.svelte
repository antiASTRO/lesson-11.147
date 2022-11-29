<script lang="ts">
	type Post = {
		userId: number,
		id: number
		title: string;
		body: string;
	};

	let post: Post[] = []

	let promise: Promise<Response> = fetch('https://jsonplaceholder.typicode.com/posts')

	promise.then(res => res.text())
		   .then(text => {
			const array = JSON.parse(text)
			post = array
		   })
		   
		   function remove(id: number) {
			post = post.filter(post => post.id != id)
		   }

</script>

<h1> Posts </h1>

<div class="d-flex gap-2 flex-wrap">
	{#each post as item}
		<div class="card m-2" style="width: 250px">
			<div class="card-body">
				<h3>{item.id} {item.title}</h3>
				<p>{item.body}</p>
				<button on:click={ () => remove(item.id) } class="btn btn-primary"> Delete </button>
			</div>
		</div>
	{/each}
</div>
