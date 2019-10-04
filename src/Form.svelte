<script>
  export let quizName = "Fun Quiz 35487";
  let name = "";
  let email = "";
  let password = "";

  $: nameEmail = (() => {
    return [...name.split(""), ...email.split("")].join("and");
  })();

  function onSubmit(e) {
    e.preventDefault();
    window.alert(`
    name: ${name}
    email: ${email}
    password: ${password}
    nameEmail: ${nameEmail}
      `);
  }
</script>

<h2>The name of this quiz is {quizName}</h2>
<form on:submit={onSubmit}>
  <div>
    <label for="name">Name:</label>
    <input type="text" name="name" bind:value={name} />
  </div>
  <div>
    <label for="email">Email:</label>
    <input type="email" name="email" bind:value={email} />
  </div>
  <div>
    <label for="password">Password</label>
    <input type="password" name="password" bind:value={password} />
  </div>
  <button type="submit">Submit</button>
</form>
