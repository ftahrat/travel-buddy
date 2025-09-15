<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Travel Connections</title>
    <style>
        body {
            font-family: 'Poppins', Arial, sans-serif;
            background: linear-gradient(to right, #ffe6f0, #e6f7ff);
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #ff3366;
            margin-bottom: 20px;
        }
        form, .match-section {
            background-color: #ffffffcc;
            padding: 25px;
            border-radius: 15px;
            display: inline-block;
            margin-bottom: 20px;
            box-shadow: 0 8px 16px rgba(0,0,0,0.2);
        }
        input, select, button {
            display: block;
            margin: 12px auto;
            padding: 12px;
            width: 80%;
            border-radius: 8px;
            border: 1px solid #ccc;
            font-size: 16px;
        }
        button {
            background: linear-gradient(to right, #ff6699, #ff3366);
            color: white;
            border: none;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        #matches {
            margin-top: 20px;
            font-weight: bold;
            color: #333;
            word-break: break-word;
            max-height: 400px;
            overflow-y: auto;
            padding: 10px;
            background-color: #fff3f6;
            border-radius: 10px;
            text-align: left;
        }
        #matches li {
            margin: 8px 0;
        }
    </style>
</head>
<body>

<h1>Student Travel Connections</h1>

<form id="travelForm">
    <input type="text" id="name" placeholder="Your Name" required>
    <input type="email" id="email" placeholder="Your Email" required>

    <label for="destination">Choose your destination:</label>
    <select id="destination" required>
        <option value="">--Select a destination--</option>
        <option value="Austria">Austria</option>
        <option value="Belgium">Belgium</option>
        <option value="Croatia">Croatia</option>
        <option value="Cyprus">Cyprus</option>
        <option value="Czech Republic">Czech Republic</option>
        <option value="Denmark">Denmark</option>
        <option value="Finland">Finland</option>
        <option value="France">France</option>
        <option value="Germany">Germany</option>
        <option value="Greece">Greece</option>
        <option value="Iceland">Iceland</option>
        <option value="Ireland">Ireland</option>
        <option value="Italy">Italy</option>
        <option value="Luxembourg">Luxembourg</option>
        <option value="Montenegro">Montenegro</option>
        <option value="Malta">Malta</option>
        <option value="Albania">Albania</option>
        <option value="Netherlands">Netherlands</option>
        <option value="Norway">Norway</option>
        <option value="Poland">Poland</option>
        <option value="Portugal">Portugal</option>
        <option value="Romania">Romania</option>
        <option value="Serbia">Serbia</option>
        <option value="Spain">Spain</option>
        <option value="Sweden">Sweden</option>
        <option value="Switzerland">Switzerland</option>
        <option value="Turkey">Turkey</option>
        <option value="Georgia">Georgia</option>
        <option value="London">London</option>
    </select>

    <select id="londonTrips" style="display:none;">
        <option value="">--Select a day trip--</option>
        <option value="Stonehenge">Stonehenge</option>
        <option value="Cambridge">Cambridge</option>
        <option value="Oxford">Oxford</option>
        <option value="Bath">Bath</option>
        <option value="Brighton">Brighton</option>
        <option value="Windsor">Windsor</option>
    </select>

    <button type="submit">Join Travel Pool</button>
</form>

<div class="match-section">
    <label for="matchDestination">Select destination to see all students:</label>
    <select id="matchDestination">
        <option value="">--Select a destination--</option>
        <option value="Austria">Austria</option>
        <option value="Belgium">Belgium</option>
        <option value="Croatia">Croatia</option>
        <option value="Cyprus">Cyprus</option>
        <option value="Czech Republic">Czech Republic</option>
        <option value="Denmark">Denmark</option>
        <option value="Finland">Finland</option>
        <option value="France">France</option>
        <option value="Germany">Germany</option>
        <option value="Greece">Greece</option>
        <option value="Iceland">Iceland</option>
        <option value="Ireland">Ireland</option>
        <option value="Italy">Italy</option>
        <option value="Luxembourg">Luxembourg</option>
        <option value="Montenegro">Montenegro</option>
        <option value="Malta">Malta</option>
        <option value="Albania">Albania</option>
        <option value="Netherlands">Netherlands</option>
        <option value="Norway">Norway</option>
        <option value="Poland">Poland</option>
        <option value="Portugal">Portugal</option>
        <option value="Romania">Romania</option>
        <option value="Serbia">Serbia</option>
        <option value="Spain">Spain</option>
        <option value="Sweden">Sweden</option>
        <option value="Switzerland">Switzerland</option>
        <option value="Turkey">Turkey</option>
        <option value="Georgia">Georgia</option>
        <option value="London">London</option>
    </select>
    <button id="showBtn">Show Students</button>
</div>

<ul id="matches"></ul>
<script>
    const scriptURL = 'https://script.google.com/macros/s/AKfycbxoT9KfYuObqM6ZP2WCsV6JRQ0iA_ylms2_6X31JPKRd1Wm3HQgF6_u9XaCGQEQUl-0/exec'; // <-- Replace with your actual script URL

    // Handle form submission to Google Sheets
        document.getElementById('travelForm').addEventListener('submit', function(e){
        e.preventDefault();

        const name = document.getElementById('name').value.trim();
        const email = document.getElementById('email').value.trim();
        const destination = document.getElementById('destination').value.trim();
        const dayTrip = document.getElementById('londonTrips').value.trim();

        const formData = new FormData();
        formData.append('name', name);
        formData.append('email', email);
        formData.append('destination', destination);
        formData.append('dayTrip', dayTrip);

        fetch(scriptURL, { method: 'POST', body: formData })
            .then(response => {
                alert("You have joined the travel pool!");
                document.getElementById('travelForm').reset();
                document.getElementById('londonTrips').style.display = 'none';
            })
            .catch(error => {
                console.error('Error!', error.message);
                alert("There was an error submitting the form.");
            });
    });

    // Show London day trips if London is selected
    document.getElementById('destination').addEventListener('change', function() {
        document.getElementById('londonTrips').style.display = this.value.toLowerCase() === 'london' ? 'block' : 'none';
    });

    // You can remove or comment out the 'showBtn' listener since it's only showing local data
    // document.getElementById('showBtn').addEventListener('click', function(){
    //     alert("This feature only works with local storage. To use it with Google Sheets, you'll need Apps Script to read the sheet.");
    // });
</script>



</body>
</html>

