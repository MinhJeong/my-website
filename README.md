<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Learn English Flashcards & Quiz</title>
  <style>
    /* Basic Reset */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      background-color: #f2f2f7;
      color: #333;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 20px;
    }

    h1 {
      font-size: 2.5rem;
      font-weight: 600;
      color: #333;
      margin-bottom: 20px;
    }

    /* Menu Style */
    .menu {
      display: flex;
      flex-direction: column;
      gap: 20px;
      text-align: center;
      padding: 20px;
      border-radius: 15px;
      background-color: #fff;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
    }

    .menu button {
      font-size: 18px;
      padding: 12px 25px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .menu button:hover {
      background-color: #45a049;
    }

    /* Back to Menu Button */
    .back-button {
      margin-top: 20px;
      font-size: 16px;
      padding: 10px 15px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .back-button:hover {
      background-color: #2980b9;
    }

    /* Container for each section */
    .container {
      width: 100%;
      max-width: 1000px;
      margin-top: 30px;
    }

    .flashcard-container,
    .quiz-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
    }

    .flashcard {
      width: 200px;
      height: 250px;
      margin: 10px;
      border-radius: 15px;
      background-color: #fff;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
      font-size: 22px;
      cursor: pointer;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      position: relative;
      transform-style: preserve-3d;
    }

    .flashcard:hover {
      transform: scale(1.05);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
    }

    .flashcard .front,
    .flashcard .back {
      position: absolute;
      backface-visibility: hidden;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 18px;
      color: #333;
      border-radius: 15px;
      padding: 20px;
      font-weight: 500;
      transition: all 0.3s ease;
    }

    .flashcard .front {
      background-color: #ffffff;
    }

    .flashcard .back {
      background-color: #fffae6;
      transform: rotateY(180deg);
    }

    .flashcard.flip {
      transform: rotateY(180deg);
    }

    /* Edit and delete buttons */
    .flashcard .delete-btn,
    .flashcard .edit-btn {
      position: absolute;
      top: 10px;
      right: 10px;
      background-color: rgba(0, 0, 0, 0.6);
      color: white;
      border: none;
      padding: 5px 12px;
      font-size: 14px;
      border-radius: 25px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .flashcard .edit-btn {
      background-color: #4CAF50;
    }

    .flashcard .delete-btn {
      background-color: #e74c3c;
    }

    .flashcard .delete-btn:hover,
    .flashcard .edit-btn:hover {
      background-color: rgba(0, 0, 0, 0.8);
    }

    /* Input container for flashcards */
    .input-container {
      display: flex;
      flex-direction: column;
      justify-content: center;
      margin-top: 20px;
      gap: 15px;
    }

    .input-row {
      display: flex;
      gap: 15px;
    }

    .input-container input,
    .input-container button {
      font-size: 16px;
      padding: 10px 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
    }

    .input-container input:focus,
    .input-container button:focus {
      outline: none;
      border-color: #4CAF50;
    }

    .input-container button {
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .input-container button:hover {
      background-color: #45a049;
    }

    /* Error message */
    .error-message {
      color: #e74c3c;
      font-size: 14px;
      text-align: center;
      margin-top: 5px;
      height: 20px;
    }

    /* Quiz Section */
    .quiz-container {
      margin-top: 50px;
      text-align: center;
    }

    .quiz-container input {
      font-size: 18px;
      padding: 10px 15px;
      margin: 10px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
      width: 250px;
    }

    .quiz-container button {
      font-size: 16px;
      padding: 10px 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .quiz-container button:hover {
      background-color: #45a049;
    }

  </style>
</head>
<body>

  <h1>Learn English Flashcards & Quiz</h1>

  <!-- Menu Section -->
  <div id="menu" class="menu">
    <button onclick="showFlashcards()">Flashcards</button>
    <button onclick="showQuiz()">Quiz</button>
    <button onclick="showReverseQuiz()">Reverse Quiz (En -> Vi)</button>
  </div>

  <!-- Flashcards Section -->
  <div id="flashcards-section" class="container" style="display: none;">
    <h2>Flashcards</h2>
    <div class="flashcard-container" id="flashcard-container"></div>
    <div class="input-container">
      <div class="input-row">
        <input type="text" id="english-word" placeholder="Enter English word" />
        <input type="text" id="vietnamese-meaning" placeholder="Enter meaning in Vietnamese" />
        <button onclick="addFlashcard()">Add Flashcard</button>
      </div>
      <div id="error-message" class="error-message"></div>
    </div>
    <button class="back-button" onclick="backToMenu()">Back to Menu</button>
  </div>

  <!-- Quiz Section -->
  <div id="quiz-section" class="container" style="display: none;">
    <h2>Quiz: Translate the word</h2>
    <div class="quiz-container">
      <div id="quiz-card" class="flashcard"></div>
      <input type="text" id="quiz-answer" placeholder="Enter the English word" />
      <button onclick="checkAnswer()">Next</button>
    </div>
    <button class="back-button" onclick="backToMenu()">Back to Menu</button>
  </div>

  <!-- Reverse Quiz Section -->
  <div id="reverse-quiz-section" class="container" style="display: none;">
    <h2>Reverse Quiz: Translate English to Vietnamese</h2>
    <div class="quiz-container">
      <div id="reverse-quiz-card" class="flashcard"></div>
      <input type="text" id="reverse-quiz-answer" placeholder="Enter the Vietnamese meaning" />
      <button onclick="checkReverseAnswer()">Next</button>
    </div>
    <button class="back-button" onclick="backToMenu()">Back to Menu</button>
  </div>

  <script>
    let quizIndex = 0;
    let reverseQuizIndex = 0;
    let shuffledQuizCards = [];
    let shuffledReverseQuizCards = [];
    let flashcardsForQuiz = [];

    const quizCardElement = document.getElementById('quiz-card');
    const reverseQuizCardElement = document.getElementById('reverse-quiz-card');
    const errorMessageElement = document.getElementById('error-message');

    // Initialize flashcards from localStorage
    function initializeFlashcards() {
      flashcardsForQuiz = JSON.parse(localStorage.getItem('flashcards')) || [];
    }

    // Check if flashcard already exists
    function isDuplicateFlashcard(word, meaning) {
      const normalizedWord = word.toLowerCase().trim();
      const normalizedMeaning = meaning.toLowerCase().trim();
      
      // Check for exact match
      const exactMatch = flashcardsForQuiz.some(card => 
        card.word.toLowerCase().trim() === normalizedWord && 
        card.meaning.toLowerCase().trim() === normalizedMeaning
      );
      
      if (exactMatch) {
        return { duplicate: true, type: 'exact', message: "Flashcard này đã tồn tại!" };
      }

      // Check for English word match
      const wordMatch = flashcardsForQuiz.some(card => 
        card.word.toLowerCase().trim() === normalizedWord
      );
      
      if (wordMatch) {
        return { duplicate: true, type: 'word', message: "Từ tiếng Anh này đã có trong bộ flashcard!" };
      }

      // Check for Vietnamese meaning match
      const meaningMatch = flashcardsForQuiz.some(card => 
        card.meaning.toLowerCase().trim() === normalizedMeaning
      );
      
      if (meaningMatch) {
        return { duplicate: true, type: 'meaning', message: "Nghĩa tiếng Việt này đã có trong bộ flashcard!" };
      }

      return { duplicate: false };
    }

    // Fisher-Yates shuffle function to randomize the order of cards
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
    }

    // Initialize and shuffle the quiz cards
    function initializeQuiz() {
      shuffledQuizCards = [...flashcardsForQuiz];  // Copy original array
      shuffleArray(shuffledQuizCards);
      quizIndex = 0;  // Reset quiz index
    }

    // Initialize and shuffle the reverse quiz cards (En -> Vi)
    function initializeReverseQuiz() {
      shuffledReverseQuizCards = [...flashcardsForQuiz];  // Copy original array
      shuffleArray(shuffledReverseQuizCards);
      reverseQuizIndex = 0;  // Reset reverse quiz index
    }

    // Show flashcards in Quiz mode
    function loadQuizCard() {
      if (shuffledQuizCards.length === 0) {
        quizCardElement.innerHTML = `
          <div class="front">No flashcards available. Please add some first.</div>
        `;
        return;
      }

      if (quizIndex < shuffledQuizCards.length) {
        const flashcard = shuffledQuizCards[quizIndex];
        quizCardElement.innerHTML = `
          <div class="front">${flashcard.meaning}</div>
        `;
        document.getElementById('quiz-answer').value = '';
      } else {
        quizCardElement.innerHTML = `
          <div class="front">Quiz completed! You answered all cards.</div>
        `;
      }
    }

    // Levenshtein Distance function to calculate the similarity between the input and correct answer
    function levenshtein(a, b) {
      const tmp = [];
      for (let i = 0; i <= a.length; i++) {
        tmp[i] = [i];
      }
      for (let j = 0; j <= b.length; j++) {
        tmp[0][j] = j;
      }
      for (let i = 1; i <= a.length; i++) {
        for (let j = 1; j <= b.length; j++) {
          const cost = a[i - 1] === b[j - 1] ? 0 : 1;
          tmp[i][j] = Math.min(
            tmp[i - 1][j] + 1, // Xóa
            tmp[i][j - 1] + 1, // Thêm
            tmp[i - 1][j - 1] + cost // Thay thế
          );
        }
      }
      return tmp[a.length][b.length];
    }

    // Check the answer in Quiz mode
    function checkAnswer() {
      if (shuffledQuizCards.length === 0) {
        alert('No flashcards available. Please add some first.');
        return;
      }

      const answer = document.getElementById('quiz-answer').value.trim().toLowerCase();
      const correctAnswer = shuffledQuizCards[quizIndex].word.toLowerCase();

      const distance = levenshtein(answer, correctAnswer); // Calculate Levenshtein distance

      // If distance is 0, answer is correct
      if (distance === 0) {
        quizIndex++;
        if (quizIndex >= shuffledQuizCards.length) {
          alert('You have completed the quiz!');
          quizIndex = 0; // Reset quiz
          initializeQuiz(); // Re-shuffle for new attempt
        }
        loadQuizCard();
      } else if (distance === 1) {
        alert('You made a small mistake, try again!');
      } else {
        alert('Incorrect! Try again.');
      }
    }

    // Show flashcards in Reverse Quiz mode (En -> Vi)
    function loadReverseQuizCard() {
      if (shuffledReverseQuizCards.length === 0) {
        reverseQuizCardElement.innerHTML = `
          <div class="front">No flashcards available. Please add some first.</div>
        `;
        return;
      }

      if (reverseQuizIndex < shuffledReverseQuizCards.length) {
        const flashcard = shuffledReverseQuizCards[reverseQuizIndex];
        reverseQuizCardElement.innerHTML = `
          <div class="front">${flashcard.word}</div>
        `;
        document.getElementById('reverse-quiz-answer').value = '';
      } else {
        reverseQuizCardElement.innerHTML = `
          <div class="front">Quiz completed! You answered all cards.</div>
        `;
      }
    }

    // Check the answer in Reverse Quiz mode (En -> Vi)
    function checkReverseAnswer() {
      if (shuffledReverseQuizCards.length === 0) {
        alert('No flashcards available. Please add some first.');
        return;
      }

      const answer = document.getElementById('reverse-quiz-answer').value.trim().toLowerCase();
      const correctAnswer = shuffledReverseQuizCards[reverseQuizIndex].meaning.toLowerCase();

      // Check if answer includes part of the correct meaning
      if (correctAnswer.includes(answer)) {
        alert('Good job, you got part of the answer!');
        reverseQuizIndex++;
        if (reverseQuizIndex >= shuffledReverseQuizCards.length) {
          alert('You have completed the reverse quiz!');
          reverseQuizIndex = 0; // Reset reverse quiz
          initializeReverseQuiz(); // Re-shuffle for new attempt
        }
        loadReverseQuizCard();
      } else {
        alert('Incorrect! Try again.');
      }
    }

    // Show Flashcards, Quiz, Reverse Quiz
    function showFlashcards() {
      document.getElementById('menu').style.display = 'none';
      document.getElementById('flashcards-section').style.display = 'block';
      document.getElementById('quiz-section').style.display = 'none';
      document.getElementById('reverse-quiz-section').style.display = 'none';
      loadFlashcards(); // Load flashcards from localStorage
    }

    function showQuiz() {
      document.getElementById('menu').style.display = 'none';
      document.getElementById('flashcards-section').style.display = 'none';
      document.getElementById('quiz-section').style.display = 'block';
      document.getElementById('reverse-quiz-section').style.display = 'none';
      initializeFlashcards(); // Refresh flashcards data
      initializeQuiz(); // Initialize quiz with shuffled cards
      loadQuizCard();
    }

    function showReverseQuiz() {
      document.getElementById('menu').style.display = 'none';
      document.getElementById('flashcards-section').style.display = 'none';
      document.getElementById('quiz-section').style.display = 'none';
      document.getElementById('reverse-quiz-section').style.display = 'block';
      initializeFlashcards(); // Refresh flashcards data
      initializeReverseQuiz(); // Initialize reverse quiz with shuffled cards
      loadReverseQuizCard();
    }

    function backToMenu() {
      document.getElementById('menu').style.display = 'flex';
      document.getElementById('flashcards-section').style.display = 'none';
      document.getElementById('quiz-section').style.display = 'none';
      document.getElementById('reverse-quiz-section').style.display = 'none';
    }

    // Add flashcard functionality
    function addFlashcard() {
      const englishWord = document.getElementById('english-word').value;
      const vietnameseMeaning = document.getElementById('vietnamese-meaning').value;
      
      // Clear previous error message
      errorMessageElement.textContent = '';
      errorMessageElement.style.display = 'none';

      if (!englishWord.trim() || !vietnameseMeaning.trim()) {
        errorMessageElement.textContent = "Vui lòng nhập cả từ và nghĩa.";
        errorMessageElement.style.display = 'block';
        return;
      }

      // Check for duplicates
      const duplicateCheck = isDuplicateFlashcard(englishWord, vietnameseMeaning);
      if (duplicateCheck.duplicate) {
        errorMessageElement.textContent = duplicateCheck.message;
        errorMessageElement.style.display = 'block';
        return;
      }

      const newFlashcard = {
        id: flashcardsForQuiz.length ? flashcardsForQuiz[flashcardsForQuiz.length - 1].id + 1 : 1,
        word: englishWord.trim(),
        meaning: vietnameseMeaning.trim()
      };

      flashcardsForQuiz.push(newFlashcard);
      localStorage.setItem('flashcards', JSON.stringify(flashcardsForQuiz));

      const flashcard = createFlashcard(newFlashcard.word, newFlashcard.meaning, newFlashcard.id);
      document.getElementById('flashcard-container').appendChild(flashcard);

      // Clear input fields
      document.getElementById('english-word').value = '';
      document.getElementById('vietnamese-meaning').value = '';
    }

    function createFlashcard(word, meaning, id) {
      const flashcard = document.createElement('div');
      flashcard.classList.add('flashcard');
      flashcard.dataset.id = id;
      flashcard.innerHTML = `
        <div class="front">${word}</div>
        <div class="back">${meaning}</div>
        <button class="edit-btn" onclick="editFlashcard(${id})">Edit</button>
        <button class="delete-btn" onclick="deleteFlashcard(${id})">Delete</button>
      `;
      flashcard.onclick = () => {
        flashcard.classList.toggle('flip');
      };

      return flashcard;
    }

    // Load all flashcards from localStorage when loading Flashcards page
    function loadFlashcards() {
      initializeFlashcards(); // Refresh flashcards data
      const container = document.getElementById('flashcard-container');
      container.innerHTML = ''; // Clear the container before appending new flashcards

      if (flashcardsForQuiz.length === 0) {
        container.innerHTML = '<p>No flashcards yet. Add some using the form above.</p>';
        return;
      }

      flashcardsForQuiz.forEach(card => {
        const flashcard = createFlashcard(card.word, card.meaning, card.id);
        container.appendChild(flashcard);
      });
    }

    function deleteFlashcard(id) {
      flashcardsForQuiz = flashcardsForQuiz.filter(card => card.id !== id);
      localStorage.setItem('flashcards', JSON.stringify(flashcardsForQuiz));

      const flashcard = document.querySelector(`.flashcard[data-id="${id}"]`);
      if (flashcard) {
        flashcard.remove();
      }

      // Refresh the display if all cards are deleted
      if (flashcardsForQuiz.length === 0) {
        loadFlashcards();
      }
    }

    function editFlashcard(id) {
      const flashcard = flashcardsForQuiz.find(card => card.id === id);

      document.getElementById('english-word').value = flashcard.word;
      document.getElementById('vietnamese-meaning').value = flashcard.meaning;

      deleteFlashcard(id);
    }

    // Load the Flashcards when the page loads
    window.onload = function() {
      initializeFlashcards();
      loadFlashcards();
    };

    // Add event listener for 'Enter' key to simulate click on 'Next'
    document.getElementById('quiz-answer').addEventListener('keypress', function(event) {
      if (event.key === 'Enter') {
        checkAnswer();
      }
    });

    document.getElementById('reverse-quiz-answer').addEventListener('keypress', function(event) {
      if (event.key === 'Enter') {
        checkReverseAnswer();
      }
    });

  </script>

</body>
</html>
