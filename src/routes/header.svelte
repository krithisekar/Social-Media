<script>
	let currentPage = 'home';
</script>

<nav class="nav">
	<a href="/" class="nav-link {currentPage === 'home' ? 'active' : ''}">
		<i class="bi bi-house-door"></i> Home
	</a>
	<a href="/trending" class="nav-link {currentPage === 'trending' ? 'active' : ''}">
		<i class="bi bi-graph-up-arrow"></i> Trending topics
	</a>
	<a href="/community" class="nav-link {currentPage === 'community' ? 'active' : ''}">
		<i class="bi bi-people"></i> Community
	</a>
	<input type="text" placeholder="Search..." class="search-bar" />
	<a href="/profile" class="nav-link profile-link">
		<i class="bi bi-person-circle"></i>
	</a>
</nav>

<style>
	.nav {
		background-color: #2c3e50;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 10px;
		color: #ecf0f1;
	}
	.nav-link {
		display: flex;
		align-items: center;
		text-decoration: none;
		color: #ecf0f1;
		margin-right: 20px;
		transition: color 0.3s;
	}
	.nav-link i {
		margin-right: 8px;
	}
	.nav-link:hover,
	.nav-link.active {
		color: #1abc9c;
	}
	.search-bar {
		border: 1px solid #95a5a6;
		padding: 5px 10px;
		border-radius: 20px;
		outline: none;
		color: #2c3e50;
	}
	.profile-link {
		margin-left: auto;
	}
</style>
