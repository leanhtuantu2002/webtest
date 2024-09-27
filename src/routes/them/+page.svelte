<script>
   import { goto } from '$app/navigation'; 

   let user = {};

    async function Save() {
        let res = await fetch("http://10.0.2.14:3000/user", {
            method: "POST",
            body: JSON.stringify(user),
            headers: {
                "Content-type": "application/json",
            }
        })
        if (res.status == 201) {
            goto("/quan-ly-nguoi-dung");
        } else {
            alert('That bai');
        }
    }
</script>

<form action="" on:submit={Save}>
    <label for="full-name">Ho va Ten</label>
    <input id="full-name" type="text" bind:value={user.full_name}>

    <label for="username">Ten Dang Nhap</label>
    <input id="username" type="text" bind:value={user.username}>

    <label for="email">Nhap Email</label>
    <input id="email" type="text" bind:value={user.email}>

    <label for="mat-khau">Mat Khau</label>
    <input id="mat-khau" type="password" bind:value={user.password}>

    <button type="submit">Save</button>
</form>
