<script>
  import Button from "./UI/Button.svelte";
  import TextInput from "./UI/TextInput.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import Header from "./UI/Header.svelte";

  let title = "";
  let subtitle = "";
  let description = "";
  let imageUrl = "";
  let address = "";
  let email = "";
  let id;
  let text;
  let row;

  let meetups = [
    {
      id: "m1",
      title: "Cooding Dojo",
      subtitle: "Let's smash Svelte",
      description: "this is a little description about learning Svelte",
      imageUrl:
        "https://secure.meetupstatic.com/s/img/7223371979728590/app_download/social/fb/meetup.en.png",
      address: "27th Mernd Road, 3252 NY",
      contactEmail: "rhjd@test.net",
      isFavorite: false
    },
    {
      id: "m2",
      title: "Cloud Service",
      subtitle: "Let's Know how to use cloud serves",
      description: "this is a little description about Cloud Services",
      imageUrl:
        "https://lh3.googleusercontent.com/rgQay7gOgrMSZkwZNgY7QAWriB6u5FwYvD6l_Ha4yiZxN_UzYDU-Evfa0zCWXGaYJFc",
      address: "27th Dksk Road, 52 OR",
      contactEmail: "eusikrfk@test.net",
      isFavorite: false
    }
  ];

  function addMeetup() {
    let newMeetup = {
      id: Math.random().toString(),
      title: title,
      subtitle: subtitle,
      description: description,
      imageUrl: imageUrl,
      contactEmail: email,
      address: address
    };
    meetups = [newMeetup, ...meetups];
  }

  function toggleFavorite(event) {
    const id = event.detail;
    const updatedMeetUp = { ...meetups.find(m => m.id === id) };
    updatedMeetUp.isFavorite = !updatedMeetUp.isFavorite;
    const meetupIndex = meetups.findIndex(m => m.id === id);
    const updatedMeetUps = [...meetups];
    updatedMeetUps[meetupIndex] = updatedMeetUp;
    meetups = updatedMeetUps;
  }
</script>

<style>
  main {
    margin-top: 5rem;
  }

  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>

<Header />

<main>
  <form on:submit|preventDefault={addMeetup}>
    <TextInput
      id="title"
      label="Title"
      value={title}
      on:input={event => (title = event.target.value)} />

    <TextInput
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      on:input={event => (subtitle = event.target.value)} />

    <TextInput
      id="imageUrl"
      label="imageUrl"
      value={imageUrl}
      on:input={event => (imageUrl = event.target.value)} />

    <TextInput
      id="address"
      label="Address"
      value={address}
      on:input={event => (address = event.target.value)} />

    <TextInput
      id="email"
      label="E-mail"
      value={email}
      type={email}
      on:input={event => (email = event.target.value)} />

    <TextInput
      id="description"
      label="Description"
      controlType="textare"
      value={description}
      on:input={event => (description = event.target.value)} />
    <Button type="submit" caption="Save" />
  </form>

  <MeetupGrid {meetups} on:togglefavorite={toggleFavorite} />
</main>
