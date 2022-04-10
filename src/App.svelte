<script>
import { onMount } from 'svelte'

/**
 * Todos
 * id {number}
 * done {boolean}
 * title {string}
 */
let todos = []

// Todo Title
let title = ''

const add = () => {
	todos = [
		...todos,
		{id: todos.length, done: false, title}
	]
	// 最後にタイトルをクリア
	init()
}

let condition = null

$: fileteredTodos = (todos, condition) => {
	return condition === null ? todos : todos.filter((t) => t.done === condition);
}

onMount(() => {
	init()
});

let initFocus = null;

const init = () => {
	title = ""
	initFocus.focus();
}
</script>

<div>
	絞り込み:
	<button on:click={() => {condition = null}}>全て</button>
	<button on:click={() => {condition = false}}>未完了</button>
	<button on:click={() => {condition = true}}>完了</button>
</div>
<div>
	<!-- input入力値とtitleを紐付ける -->
	<input type="text" bind:value={title} bind:this={initFocus}>
	<button on:click={() => add()}>タスク追加</button>
</div>
<div>
	{#if todos.length === 0}
	<div>アイテムを作成してください</div>
	{:else}
	<ul>
		<!-- foreach -->
		<!-- (todo.id)と書くことでTodoとIdを紐付ける -> 変化を検知できる -->
		{#each fileteredTodos(todos, condition) as todo (todo.id)}
		<li>
			<input type="checkbox" bind:checked={todo.done}> {todo.title}
		</li>
		{/each}
	</ul>
	{/if}
</div>

<style></style>