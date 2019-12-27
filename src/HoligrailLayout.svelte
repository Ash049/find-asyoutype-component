<script>
import SearchComponent from './SearchComponent.svelte'
</script>
<body class="HolyGrail">
  <header>Country List</header>
  <div class="HolyGrail-body">
    <main class="HolyGrail-content">
    <SearchComponent />
		</main>
    <nav class="HolyGrail-nav">side nav</nav>
    <aside class="HolyGrail-ads">ads</aside>
  </div>
  <footer>@m3-ui</footer>
</body>
<style>
	body{
		background: #ECEEF1;
	  padding: 0;
		color: #2873EF;
	}
	.HolyGrail {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

.HolyGrail-body {
  display: flex;
  flex: 1;
}
	.HolyGrail-content {
    flex: 1;
		 background: #FFFFFF;
}

.HolyGrail-nav, .HolyGrail-ads {
  /* 12em is the width of the columns */
  flex: 0 0 12em;
	 background: #FFFFFF;
  margin-left: 5px;
}

.HolyGrail-nav {
  /* put the nav on the left */
  order: -1;
	background: #FFFFFF;
  margin-right: 5px;
}
	header{
    text-align: center;
    padding: 5px;
    font-size: 30px;
    font-weight: 900;
    background-color: #FFFFFF;
    margin-bottom: 5px;
}
footer{
	text-align: center;
  background: #FFFFFF;
  margin-top: 5px;
}
</style>