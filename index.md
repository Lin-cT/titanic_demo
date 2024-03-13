---
layout: base
title: Home
permalink: "/"
search_exclude: false
---
<h2>Passenger Information Form</h2>
    <form id="passengerForm">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name">
        <label for="pclass">Passenger Class:</label>
        <input type="number" id="pclass" name="pclass" >
        <label for="sex">Sex:</label>
        <input type="text" id="sex" name="sex" >
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" >
        <label for="sibsp">Number of Siblings/Spouses Aboard:</label>
        <input type="number" id="sibsp" name="sibsp">
        <label for="parch">Number of Parents/Children Aboard:</label>
        <input type="number" id="parch" name="parch">
        <label for="fare">Fare:</label>
        <input type="number" id="fare" name="fare">
        <label for="embarked">Embarked:</label>
        <input type="text" id="embarked" name="embarked" >
        <label for="alone">Alone:</label>
        <input type="text" id="alone" name="alone" >
        <button type="button" onclick="submitForm()">Submit</button>
    </form>
<script>
function submitForm() {
            var formData = {
                name: document.getElementById('name').value,
                pclass: parseInt(document.getElementById('pclass').value),
                sex: document.getElementById('sex').value,
                age: parseInt(document.getElementById('age').value),
                sibsp: parseInt(document.getElementById('sibsp').value),
                parch: parseInt(document.getElementById('parch').value),
                fare: parseFloat(document.getElementById('fare').value),
                embarked: document.getElementById('embarked').value,
                alone: document.getElementById('alone').value,
            };
            //
            fetch('YOUR_API_ENDPOINT', {
                method: 'POST', //post data/send to data to api
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(formData),
            })
            .then(response => response.json())
            .then(data => {
                console.log('API response:', data);
                // You can handle the response from the API here
            })
            .catch(error => {
                console.error('Error:', error);
            });
        }
</script>
</html>
