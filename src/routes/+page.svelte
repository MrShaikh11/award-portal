<!-- CommitteeMembersPage.svelte -->

<script>
  import { onMount } from "svelte";

  let committeeMembers = [];

  onMount(async () => {
    // Fetching data from an API (dummy data for demonstration purposes)
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    const data = await response.json();

    // Creating dummy committee members from the fetched data
    committeeMembers = data.slice(0, 5).map((user) => ({
      id: user.id,
      name: user.name,
      position: "Committee Member",
      // Generate a random placeholder image URL using Lorem Picsum
      imageUrl: `https://picsum.photos/id/${user.id}/50/50`,
    }));
  });
</script>

<div>
  <header>
    <h1>Award Portal Committee Members</h1>
  </header>

  <main>
    <h2>Committee Members</h2>
    <ul>
      {#each committeeMembers as member (member.id)}
        <li>
          <img
            src={member.imageUrl}
            alt="Committee Member"
            width="50"
            height="50"
          />
          <strong>{member.name}</strong> - {member.position}
        </li>
      {/each}
    </ul>
  </main>
</div>

<style>
  body {
    font-family: "Arial", sans-serif;
    margin: 0;
    padding: 0;
  }

  header {
    background-color: #333;
    color: white;
    padding: 1rem;
    text-align: center;
  }

  h1 {
    margin: 0;
  }

  main {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }

  h2 {
    color: #333;
    border-bottom: 2px solid #333;
    padding-bottom: 10px;
  }

  ul {
    list-style: none;
    padding: 0;
    margin-top: 20px;
  }

  li {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  }

  img {
    border-radius: 50%;
    margin-right: 15px;
  }

  strong {
    color: #3498db;
  }
</style>
