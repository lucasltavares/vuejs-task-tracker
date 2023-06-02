<template>
	<header>
		<h1>{{title}}</h1>
		<Button v-show="homePage"
		@btn-click="$emit('toggle-add-task')" 
		:text="showAddTask ? 'Close' : 'Add task'" 
		:color="showAddTask ? 'red' : 'green'" />
		<!--<Button text="Update task" color="blue" />-->
		<!--<Button text="Delete task" color="red" />-->
	</header>
</template>

<script>
	import Button from '../components/button.vue'

	export default {
		name: 'Header',
		//props: ['title'],
		components: {
			Button
		},
		computed: {
			homePage() {
				if(this.$route.path === '/') {
					return true
				} else {
					return false
				}
			}
		},
		props: {
			title: String,
			showAddTask: Boolean
		},
		emits: ['toggle-add-task']
		/*props: {
			title: {
				type: String,
				default: 'Hello World'
			}
		}*/
	}
</script>

<style scoped>
	header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20px;	
	}
	

</style>
