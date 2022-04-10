<script>
// Todo
let todos = [
	{id: 0, done: false, title: 'レストランを予約する'},
	{id: 1, done: false, title: 'サプライズ用の指輪を買う'},
	{id: 2, done: false, title: 'スポーツをする'}
]

// Todo Title
let title = ''

const add = () => {
	todos = [
		...todos,
		{id: todos.length, done: false, title}
	]
}
</script>

<div>
	絞り込み:
	<button>全て</button>
	<button>未完了</button>
	<button>完了</button>
</div>
<div>
	<!-- input入力値とtitleを紐付ける -->
	<input type="text" bind:value={title}>
	<button on:click={() => add()}>タスク追加</button>
</div>
<div>
	<ul>
		<!-- foreach -->
		<!-- (todo.id)と書くことでTodoとIdを紐付ける -> 変化を検知できる -->
		{#each todos as todo (todo.id)}
		<li>
			<input type="checkbox" bind:checked={todo.done}> {todo.title}
		</li>
		{/each}
	</ul>
</div>

<style></style>