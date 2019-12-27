<script>
	import { onMount } from "svelte";
    let q=''
	let list = [];
	let filteredList =[];
	let startsWith = (item, query) => item.toLowerCase().indexOf(query.toLowerCase()) != -1;
	onMount(async function() {
		try{
			const response = await fetch("https://restcountries.eu/rest/v2/all");
    const json = await response.json();
		list =json
		}
		catch(err){
			alert(err)
		}
    
  });
$: filteredList =  q && q.length 
					? list.filter(item=> startsWith(item.name, q)) : list;
	 
	
</script>
<div class="filtering-list">
  <div class="filter-search">
    <input bind:value={q} type="text" class="search">
  </div>
		<ul class="filter-list">
   {#each filteredList as name}
      <li>{name.name}</li>
    {/each}
  </ul>
		{#if filteredList == ''}
		<p class="filter-no-match">There is no item matching '{q}' that can be displayed.</p>
	{/if}
</div>

<style>
	.filtering-list {
		font-size: 14px;
		padding: 5px;
		
	}
	.search {
		border: 1px solid #ccc;
		border-radius: 10px;
		font-size: 14px;
		padding: 10px 8px;
		outline: none;
		width: 100%;
	}
	.filter-list {
		list-style-type: none;
		margin-left: 0;
		padding-left: 0;
	}
	.filter-list li:first-child {
		border-top-left-radius: 5px;
		border-top-right-radius: 5px;
	}
	.filter-list li:last-child {
		border-bottom-left-radius: 5px;
		border-bottom-right-radius: 5px;
	}
	.filter-list li {
		margin-bottom: -1px;
		padding: 10px;
		background-color: #fff;
		border: 1px solid #ddd;
		color: #333;
	}
	.filter-no-match {
		background-color: #ddd;
		padding: 15px;
	}

</style>
