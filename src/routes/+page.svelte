<script>
	import { onMount } from 'svelte';
	let posts = [];
	let comments = {};
	let showCommentsForPostId = null;
	onMount(async () => {
		const res = await fetch('https://jsonplaceholder.typicode.com/posts');
		posts = await res.json();
	});

	async function fetchComments(postId, userId) {
		const response = await fetch(`https://jsonplaceholder.typicode.com/comments?postId=${postId}`);
		comments[postId] = await response.json();
		showCommentsForPostId = postId;
	}

	function toggleComments(postId, userId) {
		console.log(postId, userId);
		if (showCommentsForPostId === postId) {
			showCommentsForPostId = null;
		} else {
			fetchComments(postId, userId);
		}
	}
</script>

<div class="master p-4">
	<div class="content">
		<!-- User Profile Section -->
		<div class="profile">
			<img src="https://picsum.photos/id/237/200/300" alt="" class="profilePicture img-fluid" />
			<h4>Username</h4>
		</div>
		<!-- Posts Section -->
		{#each posts as post}
			<article class="post">
				<header class="post-header">
					<h2 class="title fs-5">{post.title}</h2>
				</header>
				<p class="post-body">{post.body}</p>
				<footer class="post-footer">
					<button on:click={() => toggleComments(post.id, post.userId)} class="btn comment-button"
						>Comment</button
					>
					<button class="btn like-button">Like</button>
					<button class="btn share-button">Share</button>
					{#if showCommentsForPostId === post.id}
						<section class="comments">
							{#each comments[post.id] as comment}
								<div class="comment rounded-2">
									<strong>{comment.name}</strong> says:
									<p>{comment.body}</p>
								</div>
							{/each}
						</section>
					{/if}
				</footer>
			</article>
		{/each}
	</div>
</div>

<style>
	.master {
		background-color: #f0f2f5;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}

	.profile {
		background-color: #ffffff;
		padding: 1rem;
		border: 1px solid #ccc;
		text-align: center;
		border-radius: 10px;
		margin-bottom: 1rem;
	}

	.profilePicture {
		border-radius: 50%;
		margin-bottom: 0.5rem;
		background-color: #f0f2f5;
	}

	.post {
		background-color: #ffffff;
		border: 1px solid #ccc;
		border-radius: 10px;
		margin-bottom: 1rem;
		padding: 1rem;
	}

	.post-header h2 {
		color: #333;
		margin-bottom: 0.5rem;
	}

	.post-body {
		color: #555;
		margin-bottom: 1rem;
	}

	.post-footer {
		display: flex;
		justify-content: flex-start;
		gap: 0.5rem;
	}

	.btn {
		background-color: #2c3e50;
		color: #ffffff;
		padding: 0.5rem 1rem;
		border: none;
		border-radius: 20px;
		cursor: pointer;
		transition: background-color 0.3s;
	}

	.btn:hover {
		background-color: #1abc9c;
	}

	.comments {
		background-color: #e9ecef;
		border-top: 1px solid #ccc;
		padding: 0.5rem;
		border-radius: 0 0 10px 10px;
	}

	.comment {
		background-color: #f8f9fa;
		padding: 0.5rem;
		border-radius: 10px;
		margin-bottom: 0.5rem;
	}

	.comment-button,
	.like-button,
	.share-button {
		margin-right: 0;
		max-height: 50px;
	}
</style>
