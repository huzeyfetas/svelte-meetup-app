<script>
  import { createEventDispatcher } from "svelte";
  import TextInput from "../shared/TextInput.svelte";
  import Button from "../shared/Button.svelte";

  const dispatch = createEventDispatcher();

  let title = "";
  let subtitle = "";
  let description = "";
  let imageUrl = "";
  let address = "";
  let contactEmail = "";

  const save = (e) => {
    dispatch("savemeetup", {
      id: Math.random(),
      title,
      subtitle,
      description,
      imageUrl,
      address,
      contactEmail,
      isFav: false,
    });
  };
</script>

<form class="meetup-add-form" on:submit|preventDefault={save}>
  <TextInput
    id="title"
    label="Title"
    value={title}
    on:input={(e) => (title = e.target.value)}
  />
  <TextInput
    id="subtitle"
    label="Subtitle"
    value={subtitle}
    on:input={(e) => (subtitle = e.target.value)}
  />
  <TextInput
    id="address"
    label="Address"
    value={address}
    on:input={(e) => (address = e.target.value)}
  />
  <TextInput
    id="imageUrl"
    label="Image Url"
    value={imageUrl}
    on:input={(e) => (imageUrl = e.target.value)}
  />
  <TextInput
    id="contactEmail"
    label="E-mail"
    value={contactEmail}
    type="email"
    on:input={(e) => (contactEmail = e.target.value)}
  />
  <TextInput
    id="description"
    label="Descrition"
    value={description}
    rows="4"
    controlType="textarea"
    on:input={(e) => (description = e.target.value)}
  />

  <Button type="submit">Save</Button>
</form>

<style>
  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>
