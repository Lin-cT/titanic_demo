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
        <p><label>
            Age:
            <input type="text" name="age" id="age" required>
        </label></p>
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

<div id="probabilities">
    <p>Survival Probability: <span id="survivalProbability"></span></p>
    <p>Death Probability: <span id="deathProbability"></span></p>
</div>

<!-- Table -->
<h2>Titanic Records</h2>
<table id="userTable">
    <tr>
        <th>Name</th>
        <th>Pclass</th>
        <th>Sex</th>
        <th>Age</th>
        <th>Sibsp</th>
        <th>Parch</th>
        <th>Fare</th>
        <th>Embarked</th>
        <th>Alone?</th>
        <th>Survival Chance</th>
        <th>Death Chance</th>
    </tr>
</table>

<script>
    // User creation
    function create_user() {
        const name = document.getElementById('name').value;
        const pclass = document.getElementById('pclass').value;
        const sex = document.getElementById('sex').value;
        const age = document.getElementById('age').value;
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
            "alone": alone
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
                return response.json();
            } else {
                throw new Error('User creation failed');
            }
        })
        //pulls data of probability of surviving and dying
        .then(data => {
            const survivalProbability = data.alive_proba;
            const deathProbability = data.dead_proba;
            const survivalProbabilityNumeric = parseFloat(survivalProbability);
            const deathProbabilityNumeric = parseFloat(deathProbability);
            console.log("Survival Probability:", survivalProbabilityNumeric);
            console.log("Death Probability:", deathProbabilityNumeric);
            document.getElementById('survivalProbability').textContent = survivalProbabilityNumeric.toFixed(2);
            document.getElementById('deathProbability').textContent = deathProbabilityNumeric.toFixed(2);

            addRowToTable(formData, survivalProbabilityNumeric, deathProbabilityNumeric);
        })
        .catch(error => {
            console.error('Error:', error);
            alert("User Creation failed. Try again.");
        });
    }
    //adds data to table
    function addRowToTable(data, survivalProbability, deathProbability) {
        const table = document.getElementById('userTable');

        const row = table.insertRow(-1); // Insert a new row at the end of the table

        const cells = ['name', 'pclass', 'sex', 'age', 'sibsp', 'parch', 'fare', 'embarked', 'alone'];
        cells.forEach(cell => {
            const newCell = row.insertCell(-1);
            newCell.textContent = data[cell];
        });
        const survivalCell = row.insertCell(-1);
        survivalCell.textContent = survivalProbability.toFixed(2);
        const deathCell = row.insertCell(-1);
        deathCell.textContent = deathProbability.toFixed(2);
    }
</script>
