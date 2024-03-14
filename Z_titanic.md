---
toc: true
layout: base
search_exclude: false
permalink: titanic
courses: {compsci: {week: 26}}
---
<!-- Inputs -->
<div>
    <form>
        <p><label>
            Name:
            <input type="text" name="name" id="name" required>
        </label></p>
        <p><label>
            Age:
            <input type="text" name="age" id="age" required>
        </label></p>
        <p><label>
            Sex:
            <input type="text" name="sex" id="sex" required>
        </label></p>
        <p><label>
            Class:
            <input type="text" name="class" id="class" required>
        </label></p>
        <p><label>
            Fair:
            <input type="text" name="fair" id="fair" required>
        </label></p>
        <button type="button" onclick="create_user()">Submit</button>
    </form>
</div>

<!-- Table -->
<h2>Titanic Records</h2>
<table id="userTable">
	<tr>
		<th>Name</th>
		<th>Sex</th>
		<th>Age</th>
		<th>Class</th>
		<th>Fair</th>
		<th>Survived</th>
	</tr>
</table>

<script>
    //user creation
	function create_user(){
        const name = document.getElementById('name').value;// DEFINE VALUES
        const age =  document.getElementById('age').value;
        const sex =  document.getElementById('age').value;
        const class = document.getElementById('class').value;
        const fair = document.getElementById('fair').value;
        const formData = {
            "name": name,
            "age": age,
            "sex": sex,
            "class": class,
            "fair": fair,
            // Add other form fields as needed
        };            
        fetch('http://127.0.0.1:8086/api/titanic/', {

            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(formData)
        })
            .then(response => {
                if (response.ok) {
                suvivability()
            } else {
                console.error('User creation failed');
                alert("User Creation failed. Try again.");
            }
        })
        .catch(error => {
            console.error('Error:', error);
        });
    }

	function suvivability() {
		//run for newest created user to get suvivability outcome.
	}
</script>