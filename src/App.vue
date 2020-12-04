<template>
	<div id="App">
		<div class="container grid-xs py-2">
			<img class="img-responsive img-logo py-2" src="@/assets/coolab.svg" alt="logo coolab">
			<form @submit.prevent="addTodo(todo)" >
				<div class="input-group">
					<input type="text" v-model="todo.description" class="form-input" placeholder="Novo todo">
					<button class="btn btn-primary input-group-btn">+</button>
				</div>
			</form>
			<div class="todo-lists">
				<todo v-for="t in todos" :key="t.id" @toggle="toggleTodo" @remove="removeTodo" :todo="t"/>
			</div>
		</div>
	</div>

</template>

<script>
import Todo from './components/Todo';

export default {
	name: 'App',
	components: { Todo },
	data() {
		return { todos: [], todo: { checked: false } };
		},
	methods: {
		addTodo(todo) {
		todo.id = Date.now();
		this.todos.push(todo);
		//isso faz com que ele limpe a cada add
		this.todo = { checked: false };
		},

		toggleTodo(todo){
			const index = this.todos.findIndex(item => item.id === todo.id);
			if (index > -1) {
				const checked = !this.todos[index].checked;
				//isso não funcionou
				//this.$set(this.todos, index, {...this.todos[index], checked });
				this.todos[index].checked = checked;
			}
		},

		removeTodo(todo) {
			// const index = this.todos.findIndex(item => item.id === todo.id);
			// if (index > -1){
				this.todos = this.todos.filter(item => item.id !== todo.id);
			//}
		}
	}
};
</script>
 
<style scoped>

 .img-logo {
 max-width: 200px;
 margin: 0 auto;
 }

 .todo-lists {
	padding-top: 2rem;
 }

</style>
