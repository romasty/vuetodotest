<template>
	<div class="base">
		<h1>My TODO list</h1>
		<form class="form">
			<label>New</label>
			<input v-model="newItem" name="newItem"/>
			<button v-on:click="addItem()">Add task</button>
		</form>
		<h2 v-if="items.length > 0">Tasks: {{calcProgress()}}</h2>
		<ul>
			<li
				v-for="(item, index) in items"
				v-bind:key="index"
			>
				<Item 
					:label="item.content" :isDone="item.done"
					@delete-item="removeItem(index)"
					@do-item="setItemCompleted(item)"
				/>
			</li>
		</ul>
		<button v-if="items.length > 0" @click="clearAll()">Clear All</button>
	</div>
</template>

<script>
	import { ref } from 'vue';
    import Item from './components/Item.vue'

	export default {
		name: 'App',
        components: {
            Item
        },
		setup () {
			const newItem = ref('');
			const defaultData = [];
			const itemsData = JSON.parse(localStorage.getItem('vuetodotest')) || defaultData;
			const items = ref(itemsData);

			function addItem () {
				if (newItem.value) {
					items.value.push({
						done: false,
						content: newItem.value
					});
					newItem.value = '';
				}
				saveData();
			}

			function setItemCompleted (item) {
				item.done = !item.done;
				saveData();
			}

			function removeItem (index) {
				items.value.splice(index, 1);
				saveData();
			}

			function saveData () {
				const storageData = JSON.stringify(items.value);
				localStorage.setItem('vuetodotest', storageData);
			}

			function clearAll () {
				items.value.splice(0,items.value.length);
				saveData();
			}

			function calcProgress() {
                const doneCount = this.items.filter(item => item.done).length;
                return `${doneCount} / ${this.items.length}`;
            }

			return {
				items,
				newItem,
				addItem,
				setItemCompleted,
				removeItem,
				saveData,
				clearAll,
				calcProgress,
			}
		}
	}
</script>

<style src="@/assets/base.css"></style>
