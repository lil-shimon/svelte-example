<script>
let todos = [
	{id: 0, done: false, title: 'レストランを予約する'},
	{id: 1, done: false, title: 'サプライズ用の指輪を買う'},
	{id: 2, done: false, title: 'スポーツをする'}
]
</script>

<div>
	絞り込み:
	<button>全て</button>
	<button>未完了</button>
	<button>完了</button>
</div>
<div>
	<input type="text">
	<button>タスク追加</button>
</div>
<div>
	<ul>
		<!-- foreach -->
		{#each todos as todo (todo.id)}
		<li>
			<input type="checkbox" bind:checked={todo.done}> {todo.title}
		</li>
		{/each}
	</ul>
</div>

<style></style>