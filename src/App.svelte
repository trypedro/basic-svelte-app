<script>
  import ContactCard from "./ContactCard.svelte"
  
  let name = "Max"
  let title = ""
  let image = ""
  let description = ""
  let formState = 'empty'
  let createContact = []

  function addContact(){
    if (
      name.trim().length === 0 || 
      title.trim().length === 0 || 
      image.trim().length === 0 || 
      description.trim().length === 0
    ) {
      formState = 'invalid'
      return
    }

    createContact = [
      ...createContact ,
      { 
        id: Math.random(),
        name: name,
        jobTitle: title,
        imageUrl: image,
        desc: description
      }]
    formState = 'done'
  }   
  
  function deleteFirst(){
    createContact = createContact.slice(1)
  }

  function deleteLast(){
    createContact = createContact.slice(0, -1)
  }
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click="{addContact}">
  Add Contact Card
</button>
<button on:click="{deleteFirst}">
  Delete First
</button>
<button on:click="{() => { // example of inline functions in svelte with arrow => function
  createContact = createContact.slice(0, -1)
}}">
  Delete Last
</button>

{#if formState === 'invalid'}
  <p>Invalid input.</p>
{:else}
  <p>Please enter some data and hit the button.</p>
{/if}

{#each createContact as contact, i (contact.id)}
  <h2># {i + 1}</h2>
  <ContactCard
    userName={contact.name} 
    jobTitle={contact.jobTitle} 
    description={contact.desc} 
    userImage={contact.imageUrl} 
  />
{:else}
  <p>Please start adding some ctnacts, we found none!</p>
{/each}