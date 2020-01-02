<script>
	import { onMount } from "svelte";
    let searchingCountryName=''
	let countryNameList = [];
	let filteredCountryList =[];
	//checking for valid substring (entered searchingCountryName) of avaliable country name(countryName)
	let CountryNamestartsWith = (countryName, searchingCountryName) => countryName.toLowerCase().indexOf(searchingCountryName.toLowerCase()) != -1;
	//Fetching all the country name from API (https://restcountries.eu/rest/v2/all)
	onMount(async function() {
		try{
		const response = await fetch("https://restcountries.eu/rest/v2/all");
        const json = await response.json();
		countryNameList =json
		}
		catch(error){
			alert(error)
		}
    
  });
  //Filtering country names with respect to searched keywords(searched country name)
$: filteredCountryList =  searchingCountryName && searchingCountryName.length 
					? countryNameList.filter(countryNameObject=> CountryNamestartsWith(countryNameObject.name, searchingCountryName)) : countryNameList;
	 
	
</script>
<div class="filtering-list">
  <div class="filter-search">
    <input bind:value={searchingCountryName} type="text" class="search">
  </div>
		<ul class="filter-list">
   {#each filteredCountryList as name}
      <li>{name.name}</li>
    {/each}
  </ul>
		{#if filteredCountryList == ''}
		<p class="filter-no-match">There is no item matching '{searchingCountryName}' that can be displayed.</p>
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
