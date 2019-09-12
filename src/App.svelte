<style>
	.container {
		display: flex;
		flex-direction: column;
		width:100vw;
		height:100vh;
		overflow-y: auto;
	}
	.autoscroll {
		overflow-y:hidden;
	}
	#spacer {
		flex-basis:50vh;
		flex-shrink:0;
		/* background-color: #232323; */
	}
	.row {
		display:flex;
		flex-direction: row;
		justify-content: space-between;
		margin:1px;
		background-color: #ddd
	}
	.selected {
		background-color: yellowgreen;
	}
	.item { 
		padding:10px;
		border:none;
		background-color: transparent;
		flex-basis:100%;
		/* pointer-events: none; */
	}
	.editmode { 
		outline : 2px solid blue;
	}
	.quantity {
		width: 20vw;
		/* height:100%; */
		padding:5px;
		background-color: yellowgreen;
	}
</style>
<script>
	export let name;
	export let selectedItem = {};


	import {afterUpdate} from 'svelte'
	import * as animateScroll from "svelte-scrollto";
	import shortid from 'shortid';
	import data from './items.js';
	import Keypad from './keypad.svelte';
	import EditItem from './edit-item.svelte';

	let items = data.map(name => ({id:'A'+shortid.generate(),name, qty: ''}));
	let keypadVisible = false;
	let autoscroll = false;
	let pointerDown = false;
	export let editMode = false;

	console.table(items)

	const findItemById = id => items.find(item => item.id === id) 

	function select(e) {
		// keypadVisible = !keypadVisible;
		console.log(selectedItem.id,e.currentTarget.id )
						const el = document.getElementById(selectedItem.id).firstChild;
		if (selectedItem.id !== e.currentTarget.id) {
			el.readOnly = true;
		}
		else {
			el.readOnly = false;
			el.focus();
			el.select();
		}
			
		selectedItem = findItemById(e.currentTarget.id);

		return;
		if (editMode && selectedItem.id !== e.currentTarget.id) {
			editMode = false;
			return;
		}
		selectedItem = findItemById(e.currentTarget.id);
		if (!keypadVisible) 
			keypadVisible = true;
		else
			handleKeypadOpen();
	}

	function handleKeypadClick(e) {
		const key = e.target.innerText;
		let qty = parseInt(`${selectedItem.qty}${key}`);
		if (key === 'X') {
			editMode = true;
			const el = document.getElementById(selectedItem.id).firstChild;
			el.readOnly = false;
			el.focus();
			console.log(el);
			return;
		}
		if (key === '+')
			qty++;
		if (key === '-') {
			if (qty < 2)
				qty = 0;
			else
				qty--;
		}
		selectedItem.qty =  qty;
		items = [...items]
	}
	function handleScroll() {
		if (!autoscroll && pointerDown) {
			console.log('autoffsdds')
			keypadVisible = false;
		}
	}

	function handleKeypadOpen() {
		const selectedElement = document.getElementById(selectedItem.id);
		const bodyElement = document.getElementsByTagName('body')[0];
		console.log(selectedElement);
		const boundingRect = selectedElement.getBoundingClientRect();
		const bodyBoundingRect = bodyElement.getBoundingClientRect();
		console.log(boundingRect.bottom,  bodyBoundingRect.bottom );
		if (boundingRect.bottom > bodyBoundingRect.bottom/2) {
			autoscroll = true;
			animateScroll.scrollTo({
				container: '#container', 
				element: `#${selectedItem.id}`,
				offset:-200,
				onDone: () => setTimeout(() => {autoscroll = false},1000)
			});
		}

	}

	function handleContextMenu(e) {
		selectedItem = findItemById(e.target.parentNode.id);
		editMode = true;
		console.log(e.target,selectedItem, editMode);
			const el = document.getElementById(selectedItem.id).firstChild;
			el.readOnly = false;
		e.target.focus();
	}

</script>
{#if editMode}
	<!-- <EditItem value={selectedItem.name}/> -->
{/if}
<div id='container' class='container' class:autoscroll 
	on:scroll={handleScroll} 
	on:pointerdown={() => pointerDown = true}
	on:pointerup={() => pointerDown = false}	
>
	{#each items as item, index}
	<div id={item.id} data-name={item.name} 
		class='row' 
		class:editmode={editMode && selectedItem.id === item.id}
		class:selected={selectedItem.id === item.id} 
		on:click={select}
		on:contextmenu|preventDefault={handleContextMenu}
	>
			<input type=text readonly class='item' value={item.name}
				on:blur={() => editMode = false}
			/>
		<!-- <div {editMode} tabindex='0' type=text class='item' value={item.name} on:blur={() => editMode = true}>{item.name} </div> -->
		<div tabindex='0' class='quantity'>{item.qty}</div>
	</div>
	{/each}
	<div id='spacer'></div>
</div>
<Keypad visible={keypadVisible} on:click={handleKeypadClick} on:open={handleKeypadOpen}/>
