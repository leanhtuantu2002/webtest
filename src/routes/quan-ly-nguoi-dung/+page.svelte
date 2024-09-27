<script>
	import { onMount } from 'svelte';

	let users = [];

    async function xoa(id) {
        if (confirm("co chac muon xoa khong")) {
        let res = await fetch(`http://10.0.2.14:3000/user/${id}`, {
            method: "DELETE"
        });
        if (res.ok) {
            alert("loi ko xoa duoc")
        }
    }
}

	onMount(async () => {
		const res = await fetch('http://10.0.2.14:3000/user');
        users = (await res.json()).data;
		console.log(users);
	});
</script>


<table>
	<thead>
		<th>STT</th>
		<th>Ho va ten</th>
		<th>Usernam</th>
		<th>Email</th>
		<th>Trang thai</th>
        <th></th>
	</thead>
	<tbody>
		{#each users as user, i (i)}
			<tr>
				<td>{i + 1}</td>
				<td>{user.full_name}</td>
				<td>{user.username}</td>
				<td>{user.email}</td>
				<td>{user.active}</td>
                <td><a href="/quan-ly-nguoi-dung/{user.id}/sua">Sửa</a></td>
                    <a href={"#"} on:click={() => xoa(user.id)}>Xóa</a>
			</tr>
		{/each}
	</tbody>
</table>
