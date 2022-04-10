<script>
import { onMount } from 'svelte'
import { slide } from 'svelte/transition'

/**
 * Todos
 * id {number}
 * done {boolean}
 * title {string}
 * priority {number}
 */
let todos = []

// Todo Title
let title = ''

// Todo Priority
let priority = 0

const add = () => {
	todos = [
		...todos,
		{id: todos.length, done: false, title, priority: priority}
	]
	// 最後にタイトルをクリア
	init()
}

const deleteTodo = (todoId) => {
	todos = todos.filter(todo => todo.id !== todoId)
}

// 何も入力されていない場合は追加できない様にする
$: disabledAdd = title === ''

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

const Priorities = {
	LOW: 1,
	MIDDLE: 2,
	HIGH: 3
}

const prioritiesNames = {
	[Priorities.LOW]: '低',
	[Priorities.MIDDLE]: '中',
	[Priorities.HIGH]: '高'
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
	<select id="priority" bind:value={priority}>
		{#each Object.entries(prioritiesNames) as [value, label]}
			<option value={value}>{label}</option>
		{/each}
	</select>
	<button disabled={disabledAdd} on:click={() => add()}>タスク追加</button>
</div>
<div>
	{#if todos.length === 0}
		<div>アイテムを作成してください</div>
	{:else}
	<ul>
		<!-- foreach -->
		<!-- (todo.id)と書くことでTodoとIdを紐付ける -> 変化を検知できる -->
		{#each fileteredTodos(todos, condition) as todo (todo.id)}
		<!-- transition:slideでslide時にanimationを追加 -->
		<li transition:slide>
			<input type="checkbox" bind:checked={todo.done}> {todo.title} {todo.priority}
			<button on:click={() => deleteTodo(todo.id)}>削除</button>
		</li>
		{/each}
	</ul>
	{/if}
</div>

<style></style>