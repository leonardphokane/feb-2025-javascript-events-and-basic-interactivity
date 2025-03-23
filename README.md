<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Webpage</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    #modal {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: white;
      padding: 20px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      border-radius: 8px;
    }
    #modal-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
    }
  </style>
</head>
<body>
  <h1>Interactive Webpage</h1>

  <!-- Toggle Background Button -->
  <button id="toggle-bg-btn">Toggle Background Color</button>

  <!-- Text Size Slider -->
  <p id="slider-text">Adjust my size with the slider below!</p>
  <input type="range" id="text-slider" min="10" max="40" value="16">

  <!-- Modal Trigger -->
  <button id="open-modal-btn">Open Modal</button>
  <div id="modal-overlay"></div>
  <div id="modal">
    <p>This is a modal!</p>
    <button id="close-modal-btn">Close Modal</button>
  </div>

  <!-- Form with Validation -->
  <form id="user-form">
    <label for="name">Name (min 3 characters):</label><br>
    <input type="text" id="name" required><br><br>

    <label for="email">Email:</label><br>
    <input type="email" id="email" required><br><br>

    <label for="password">Password (min 8 characters, 1 uppercase, 1 number):</label><br>
    <input type="password" id="password" required><br><br>

    <button type="submit">Submit</button>
  </form>

  <!-- Error Message Area -->
  <div id="error-messages" style="color: red; margin-top: 20px;"></div>

  <script src="script.js"></script>
</body>
</html>




// Toggle Background Color
const toggleBgBtn = document.getElementById('toggle-bg-btn');
toggleBgBtn.addEventListener('click', () => {
  document.body.style.backgroundColor =
    document.body.style.backgroundColor === 'lightblue' ? 'white' : 'lightblue';
});

// Adjust Text Size with Slider
const textSlider = document.getElementById('text-slider');
const sliderText = document.getElementById('slider-text');
textSlider.addEventListener('input', () => {
  sliderText.style.fontSize = `${textSlider.value}px`;
});

// Modal Functionality
const openModalBtn = document.getElementById('open-modal-btn');
const closeModalBtn = document.getElementById('close-modal-btn');
const modal = document.getElementById('modal');
const modalOverlay = document.getElementById('modal-overlay');

openModalBtn.addEventListener('click', () => {
  modal.style.display = 'block';
  modalOverlay.style.display = 'block';
});

closeModalBtn.addEventListener('click', () => {
  modal.style.display = 'none';
  modalOverlay.style.display = 'none';
});

modalOverlay.addEventListener('click', () => {
  modal.style.display = 'none';
  modalOverlay.style.display = 'none';
});

// Form Validation
const form = document.getElementById('user-form');
const errorMessages = document.getElementById('error-messages');

form.addEventListener('submit', (e) => {
  e.preventDefault(); // Prevent form submission

  const name = document.getElementById('name').value;
  const email = document.getElementById('email').value;
  const password = document.getElementById('password').value;

  let errors = [];

  if (name.length < 3) {
    errors.push('Name must be at least 3 characters long.');
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email)) {
    errors.push('Please enter a valid email address.');
  }

  const passwordRegex = /^(?=.*[A-Z])(?=.*\d).{8,}$/;
  if (!passwordRegex.test(password)) {
    errors.push(
      'Password must be at least 8 characters long, with one uppercase letter and one number.'
    );
  }

  if (errors.length > 0) {
    errorMessages.innerHTML = errors.join('<br>');
  } else {
    errorMessages.innerHTML = 'Form submitted successfully!';
    form.reset(); // Reset the form
  }
});
