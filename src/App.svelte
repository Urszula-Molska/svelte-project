<script>
  import data from './data.json';
  let posts= data.data;
  let active=1;
  let number= 1;
  let author= '';
  let post='';
  
function changeActive(activeNum) {
  active = activeNum
}

function addPost() {
  const _post = {
     id: posts.length+1, author: author,  post: post,
  }
  posts.push(_post)
  posts=posts
  author=""
  post=""
}

  function add5 () {
    number +=5
  }
  $: multiple= number*2

</script>
<header>
  <div class="join mb-10">
  <button on:click="{()=>changeActive(1)}" class="btn-secondary join-item {active===1 ? 'btn-active' : ''}">Button</button>
  <button on:click="{()=>changeActive(2)}" class="btn-secondary join-item {active===2 ? 'btn-active' : ''}">Button</button>
  <button on:click="{()=>changeActive(3)}" class="btn-secondary join-item {active===3 ? 'btn-active' : ''}">Button</button>
</div>
</header>

<main class="flex flex-col space-y-4  items-center ">
  <h1>Add post</h1>
  <div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Author</span>
  </label>
  <input bind:value="{author}" name="author" type="text" placeholder="Author" class="input input-bordered w-full max-w-xs" />
  <label class="label">
    <span  class="label-text">Post</span>
  </label>
  <textarea bind:value="{post}" name="post" class="textarea textarea-bordered h-24" placeholder="Post"></textarea>
  <button on:click="{addPost}" class="mt-4 btn btn-active btn-primary">Submit</button>
</div>
<div class="overflow-auto space-y-4 p-4">
  {#each posts.reverse() as post}
  <div class="card w-96 shadow-xl bg-pink-100">
  <div class="card-body">
    <h2 class="card-title">{post.author}</h2>
    <p>{post.post}</p>
  </div>
</div>
  {/each}
</div>
 <p> The number is: {number}</p>
  <button on:click="{add5}" class="btn btn-primary">Add five</button>
  <p> The number multiplied by 2 is {multiple}</p>
  {#if multiple <10}
  <div class="alert alert-success">
  <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
  <span>Numbers look good!</span>
</div>
{:else}
<div class="alert alert-error">
  <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
  <span>Numbers are too high!</span>
</div>
{/if}

</main>

<style>

</style>
