# koach-project
contact list 


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact List App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-color: #f4f4f4;
    }
    h1 {
      text-align: center;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
    }
    .input-field {
      display: flex;
      flex-direction: column;
      margin-bottom: 10px;
    }
    input {
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      padding: 10px 15px;
      background-color: #007BFF;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 10px;
    }
    button:hover {
      background-color: #0056b3;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      background-color: #fff;
      margin-bottom: 10px;
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }
    .delete-btn {
      background-color: #ff4d4d;
      padding: 5px 10px;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .delete-btn:hover {
      background-color: #cc0000;
    }
  </style>
</head>
<body>

  <h1>Contact List</h1>

  <div class="container">
    <div class="input-field">
      <label for="name">Name:</label>
      <input type="text" id="name" placeholder="Enter name">
    </div>
    <div class="input-field">
      <label for="phone">Phone Number:</label>
      <input type="text" id="phone" placeholder="Enter phone number">
    </div>
    <button id="addContactBtn">Add Contact</button>

    <h2>Contact List</h2>
    <ul id="contactList"></ul>
  </div>

  <script>
    // Get references to the HTML elements
    const contactList = document.getElementById('contactList');
    const nameInput = document.getElementById('name');
    const phoneInput = document.getElementById('phone');
    const addContactBtn = document.getElementById('addContactBtn');

    // Array to store contacts
    let contacts = [];

    // Function to add a contact
    function addContact() {
      const name = nameInput.value.trim();
      const phone = phoneInput.value.trim();

      // Check if the fields are not empty
      if (name === '' || phone === '') {
        alert('Please enter both name and phone number');
        return;
      }

      // Create a new contact object and add it to the contacts array
      const contact = {
        id: Date.now(), // Unique ID based on the current time
        name: name,
        phone: phone
      };
      contacts.push(contact);

      // Update the contact list display
      updateContactList();

      // Clear the input fields
      nameInput.value = '';
      phoneInput.value = '';
    }

    // Function to delete a contact
    function deleteContact(id) {
      // Remove the contact from the array by filtering out the one with the matching ID
      contacts = contacts.filter(contact => contact.id !== id);

      // Update the contact list display
      updateContactList();
    }

    // Function to update the contact list in the DOM
    function updateContactList() {
      // Clear the current list
      contactList.innerHTML = '';

      // Loop through the contacts array and create a list item for each contact
      contacts.forEach(contact => {
        const li = document.createElement('li');
        li.innerHTML = `
          <span>${contact.name} - ${contact.phone}</span>
          <button class="delete-btn" onclick="deleteContact(${contact.id})">Delete</button>
        `;
        contactList.appendChild(li);
      });
    }

    // Add event listener to the "Add Contact" button
    addContactBtn.addEventListener('click', addContact);
  </script>

</body>
</html>
