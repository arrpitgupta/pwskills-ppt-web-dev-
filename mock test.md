Question 2-Create a app where you have an input box and whenever a user types something in the input box and hits submit it should be added on the webpage below the input box
<!DOCTYPE html>
<html>
<head>
</head>
<body>
  <input type="text" id="inputText" placeholder="Enter text">
  <button id="submitButton">Submit</button>
  <div id="output"></div>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      var inputText = document.getElementById("inputText");
      var submitButton = document.getElementById("submitButton");
      var output = document.getElementById("output");

      submitButton.addEventListener("click", function() {
        var text = inputText.value;
        if (text !== "") {
          var paragraph = document.createElement("p");
          paragraph.textContent = text;
          output.appendChild(paragraph);
          inputText.value = "";
        }
      });
    });
  </script>
</body>
</html>

Question 3-Fetch data from the JSON placeholder API and display it in the browser. Also, implement the skeleton loader which will be displayed when the data is getting fetched. (No library should be used for implementing the skeleton loader

<!DOCTYPE html>
<html>
<head>
  <style>
    .skeleton-loader {
      height: 20px;
      background-color: #ddd;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <div id="userList"></div>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      var userList = document.getElementById("userList");
      var skeletonLoader = '<div class="skeleton-loader"></div>';

      // Display the skeleton loader while data is being fetched
      userList.innerHTML = skeletonLoader.repeat(10);

      fetch("https://jsonplaceholder.typicode.com/users")
        .then(function(response) {
          return response.json();
        })
        .then(function(data) {
          // Clear the skeleton loader
          userList.innerHTML = "";

          // Iterate over the fetched data and display it
          data.forEach(function(user) {
            var userElement = document.createElement("div");
            userElement.textContent = user.name;
            userList.appendChild(userElement);
          });
        })
        .catch(function(error) {
          console.log("An error occurred: ", error);
        });
    });
  </script>
</body>
</html>

Question 4-Build a responsive Navbar, on smaller screens it should be a hamburger menu which on click should reveal the menu items nicely, and on larger screens they should be displayed directly on the screen.

<!DOCTYPE html>
<html>
<head>
  <style>
    /* Navbar styles */
    .navbar {
      background-color: #333;
      color: #fff;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px;
    }

    .navbar-brand {
      font-weight: bold;
      font-size: 1.5rem;
    }

    .navbar-menu {
      display: flex;
      align-items: center;
    }

    .navbar-menu ul {
      list-style-type: none;
      margin: 0;
      padding: 0;
      display: flex;
    }

    .navbar-menu li {
      margin-right: 10px;
    }

    .navbar-menu a {
      color: #fff;
      text-decoration: none;
      padding: 5px;
    }

    /* Hamburger menu styles */
    .hamburger {
      display: none;
      cursor: pointer;
    }

    .hamburger span {
      display: block;
      width: 25px;
      height: 3px;
      background-color: #fff;
      margin-bottom: 5px;
    }

    /* Media query for smaller screens */
    @media (max-width: 768px) {
      .navbar-menu ul {
        flex-direction: column;
        display: none;
      }

      .navbar-menu.open ul {
        display: flex;
      }

      .navbar-menu li {
        margin-right: 0;
        margin-bottom: 10px;
      }

      .hamburger {
        display: block;
      }
    }
  </style>
</head>
<body>
  <nav class="navbar">
    <div class="navbar-brand">My Website</div>
    <div class="navbar-menu">
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Services</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
      <div class="hamburger">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </nav>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      var navbarMenu = document.querySelector(".navbar-menu");
      var hamburger = document.querySelector(".hamburger");

      hamburger.addEventListener("click", function() {
        navbarMenu.classList.toggle("open");
      });
       });
  </script>
</body>
</html>

Question 5- Create a form with proper form validation using JavaScript (name, email, phone number, password, age, gender, date, color picker)

<!DOCTYPE html>
<html>
<head>
  <title>Form with Basic Validation</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
    }

    h1 {
      text-align: center;
    }

    form {
      max-width: 400px;
      margin: 0 auto;
      padding: 20px;
      background-color: #f2f2f2;
      border-radius: 5px;
    }

    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }

    input[type="text"],
    input[type="email"],
    input[type="tel"],
    input[type="password"],
    input[type="number"],
    select {
      width: 100%;
      padding: 8px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }

    small {
      display: block;
      margin-top: 5px;
      color: #777;
    }

    button[type="submit"] {
      background-color: #4CAF50;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    .error {
      color: red;
    }
  </style>
</head>
<body>
  <h1>Form with Basic Validation</h1>

  <form id="myForm" onsubmit="validateForm(event)">
    <div>
      <label for="name">Name:</label>
      <input type="text" id="name" required>
    </div>

    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" required>
    </div>

    <div>
      <label for="phone">Phone Number:</label>
      <input type="tel" id="phone" pattern="[0-9]{10}" required>
      <small>Format: 1234567890</small>
    </div>

    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" required>
    </div>

    <div>
      <label for="age">Age:</label>
      <input type="number" id="age" min="18" max="99" required>
    </div>

    <div>
      <label for="gender">Gender:</label>
      <select id="gender" required>
        <option value="">Select</option>
        <option value="male">Male</option>
        <option value="female">Female</option>
        <option value="other">Other</option>
      </select>
    </div>

    <div>
      <label for="date">Date:</label>
      <input type="date" id="date" required>
    </div>

    <div>
      <label for="color">Favorite Color:</label>
      <input type="color" id="color" required>
    </div>

    <button type="submit">Submit</button>
  </form>

  <script>
    function validateForm(event) {
      event.preventDefault();
      
      // Reset any previous error messages
      const errorElements = document.getElementsByClassName('error');
      for (let i = 0; i < errorElements.length; i++) {
        errorElements[i].style.display = 'none';
      }

      // Get form values
      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const phone = document.getElementById('phone').value;
      const password = document.getElementById('password').value;
      const age = document.getElementById('age').value;
      const gender = document.getElementById('gender').value;
      const date = document.getElementById('date').value;
      const color = document.getElementById('color').value;

      // Perform validation
      if (name === '') {
        displayError('name', 'Name is required.');
      }

      if (!validateEmail(email)) {
        displayError('email', 'Invalid email format.');
      }

      if (!validatePhoneNumber(phone)) {
        displayError('phone', 'Invalid phone number format.');
      }

      if (password.length < 8) {
        displayError('password', 'Password must be at least 8 characters long.');
      }

      if (age < 18 || age > 99) {
        displayError('age', 'Age must be between 18 and 99.');
      }

      if (gender === '') {
        displayError('gender', 'Gender is required.');
      }

      // If there are no errors, submit the form
      if (document.getElementsByClassName('error').length === 0) {
        document.getElementById('myForm').submit();
      }
    }

    function displayError(fieldId, errorMessage) {
      const errorElement = document.createElement('span');
      errorElement.className = 'error';
      errorElement.innerHTML = errorMessage;
      const field = document.getElementById(fieldId);
      field.parentNode.insertBefore(errorElement, field.nextSibling);
    }

    function validateEmail(email) {
      const emailRegex = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
      return emailRegex.test(email);
    }

    function validatePhoneNumber(phone) {
      const phoneRegex = /^\d{10}$/;
      return phoneRegex.test(phone);
    }
  </script>
</body>
</html>

Question 6-Create a custom modal window using HTML, CSS, and JavaScript. On clicking a button the modal window should appear and the user can click outside the modal window to close the modal along with a close button which is inside the modal. Also when the modal is open the window should not be scrollable

<!DOCTYPE html>
<html>
<head>
  <title>Custom Modal Window</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    .modal-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      z-index: 9999;
    }

    .modal {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: #fff;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
      z-index: 10000;
    }

    .modal-close {
      position: absolute;
      top: 10px;
      right: 10px;
      cursor: pointer;
    }

    .modal-content {
      max-height: 400px;
      overflow-y: auto;
    }

    .open-modal-button {
      padding: 10px 20px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Custom Modal Window</h1>

  <button class="open-modal-button" onclick="openModal()">Open Modal</button>

  <div class="modal-overlay" onclick="closeModal()"></div>

  <div class="modal">
    <div class="modal-close" onclick="closeModal()">&times;</div>
    <div class="modal-content">
      <h2>Modal Content</h2>
      <p>This is the content of the modal window.</p>
      <p>You can add any HTML content here.</p>
    </div>
  </div>

  <script>
    const modalOverlay = document.querySelector('.modal-overlay');
    const modal = document.querySelector('.modal');

    function openModal() {
      modalOverlay.style.display = 'block';
      modal.style.display = 'block';
      document.body.style.overflow = 'hidden';
    }

    function closeModal() {
      modalOverlay.style.display = 'none';
      modal.style.display = 'none';
      document.body.style.overflow = 'auto';
    }
  </script>
</body>
</html>




