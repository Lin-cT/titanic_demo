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
            Pclass:
            <input type="text" name="pclass" id="pclass" required>
        </label></p>
        <p><label>
            Sex:
            <input type="text" name="sex" id="sex" required>
        </label></p>
            Age:
            <input type="text" name="age" id="age" required>
        <p><label>
            Sibsp:
            <input type="text" name="sibsp" id="sibsp" required>
        </label></p>
        <p><label>
            Parch:
            <input type="text" name="parch" id="parch" required>
        </label></p>
        <p><label>
            Fare:
            <input type="text" name="fare" id="fare" required>
        </label></p>
        <p><label>
            Embarked:
            <input type="text" name="embarked" id="embarked" required>
        </label></p>
        <p><label>
            Alone:
            <input type="text" name="alone" id="alone" required>
        </label></p>
        <button type="button" onclick="create_user()">Submit</button>
    </form>
</div>

<!-- Table -->
<h2>Titanic Records</h2>
<table id="userTable">
	<tr>
		<th>Name</th>
        <th>pclass</th>
		<th>Sex</th>
		<th>Age</th>
		<th>Sibsp</th>
		<th>Parch</th>
		<th>Fare</th>
        <th>Embarked</th>
        <th>Alone?</th>
	</tr>
</table>

<script>
    //user creation
	function create_user(){
        const name = document.getElementById('name').value;// DEFINE VALUES
        const pclass =  document.getElementById('pclass').value;
        const sex =  document.getElementById('sex').value;
        const age =  document.getElementById('age').value;
        const sibsp = document.getElementById('sibsp').value;
        const parch = document.getElementById('parch').value;
        const fare = document.getElementById('fare').value;
        const embarked = document.getElementById('embarked').value;
        const alone = document.getElementById('alone').value;
        const formData = {
            "name": name,
            "pclass": pclass,
            "sex": sex,
            "age": age,
            "sibsp": sibsp,
            "parch": parch,
            "fare": fare,
            "embarked": embarked,
            "alone": alone,
            // Add other form fields as needed
        };            
        fetch('http://127.0.0.1:8086/api/jokes/create', {

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

	function survivability(user) {
    //run for newest created user to get suvivability outcome.
    }
</script>