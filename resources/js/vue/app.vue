<template>
  <div class="todoListContainer">
		<div class="heading">
				<h2 id="title">Todo List</h2>
				
				<add-item-form 				
					v-on:reloadlist="getList()"
				/>
				
				
		</div>
		<list-view 
			:items="items"
			v-on:reloadlist="getList()"
		/>
      
  </div>
</template>

<script>
import addItemForm from "./addItemForm"
import listItem from './listItem.vue'
import ListView from "./ListView"

export default {
    components : {
        addItemForm,
        ListView,
        listItem,
    },
    data: function () {
        return {
            items: []
        }
    },
    methods: {
        getList () {
            axios.get('api/items')
            .then ( response => {
                this.items = response.data
            })
            .catch ( error => {
                console.log( error )
            })
        }
    },
    created () {
        this.getList();
    }
}
</script>

<style>
.todoListContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #e6e6e6;
    padding: 10px;
}

#title {
    text-align: center;
}

</style>