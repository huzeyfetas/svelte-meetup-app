<script>
  import Header from "./shared/Header.svelte";
  import MeetupGrid from "./meetups/MeetupGrid.svelte";
  import Button from "./shared/Button.svelte";
  import EditMeetup from "./meetups/EditMeetup.svelte";

  let meetups = [
    {
      id: "m1",
      title: "Coding Bootcamp",
      subtitle: "Learn to code in 2 hours",
      description:
        "In this meetup, we will have some experts that teach you how to code!",
      imageUrl:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Caffe_Nero_coffee_bar%2C_High_St%2C_Sutton%2C_Surrey%2C_Greater_London.JPG/800px-Caffe_Nero_coffee_bar%2C_High_St%2C_Sutton%2C_Surrey%2C_Greater_London.JPG",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "code@test.com",
      isFav: false,
    },
    {
      id: "m2",
      title: "Swim Together",
      subtitle: "Let's go for some swimming",
      description: "We will simply swim some rounds!",
      imageUrl:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/6/69/Olympic_swimming_pool_%28Tbilisi%29.jpg/800px-Olympic_swimming_pool_%28Tbilisi%29.jpg",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "swim@test.com",
      isFav: false,
    },
  ];

  let mode = "";

  const favoritetoggleHandler = (dispatchEvent) => {
    let id = dispatchEvent.detail;
    meetups.map((m) => {
      if (m.id === id) {
        m.isFav = !m.isFav;
      }
    });
    meetups = [...meetups];
  };

  const savemeetupHandler = (dispatchEvent) => {
    let meetupData = dispatchEvent.detail;
    meetups = [{ ...meetupData }, ...meetups];
    mode = "";
  };

  const changeMode = (e) => {
    if (mode === "") {
      mode = "add";
    } else {
      mode = "";
    }
  };
</script>

<Header />

<main>
  <Button on:click={changeMode}>{mode === "add" ? "Cancel" : "Add"}</Button>
  {#if mode === "add"}
    <EditMeetup on:savemeetup={savemeetupHandler} />
  {/if}
  <MeetupGrid {meetups} on:favoritetoggle={favoritetoggleHandler} />
</main>

<style>
  main {
    margin-top: 5rem;
  }
</style>
