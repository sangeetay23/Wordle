## Wordle Game Documentation

This documentation explains the structure and functionality of the Wordle game implemented in HTML, CSS, and JavaScript.

### index.html

- **Basic HTML Structure:**
    - Sets up the basic HTML document with `<!DOCTYPE html>`, `html`, `head`, and `body` tags.
    - Sets the language to English using `lang="en"`.
- **Head Section:**
    - Includes character set declaration using `meta charset="UTF-8"`.
    - Configures viewport meta tag (`meta name="viewport" content="width=device-width, initial-scale=1.0"`) for responsive design.
    - Links the external CSS stylesheet (`<link rel="stylesheet" href="style.css" />`).
    - Sets the document title to "Wordle" using `title="Wordle"`.
- **Body Section:**
    - Contains the following elements:
        - `<h1>Wordle</h1>`: The main heading of the game.
        - `<p>Find the hidden word - Press a letter</p>`: Instructions for the player.
        - `<div class="game-container">`: Contains the game elements:
            - `<svg>`: Represents the hangman figure, dynamically updated based on incorrect guesses.
            - `<div class="wrong-letters-container">`: Displays the incorrectly guessed letters.
            - `<div class="word" id="word">`: Displays the word to be guessed, with empty spaces for unguessed letters.
        - `<div class="popup-container" id="popup-container">`: A popup container to display win/lose messages, hidden initially.
            - `<div class="popup">`: Contains the win/lose messages and a "Play Again" button.
        - `<div class="notification-container" id="notification-container">`: A notification container to display messages like "You have already entered this letter", hidden initially.
    - Includes the external JavaScript file (`<script src="script.js"></script>`).

### script.js

- **Variables:**
    - `wordElement`: References the `<div class="word" id="word">` element.
    - `wrongLettersElement`: References the `<div class="wrong-letters-container">` element.
    - `playAgainButton`: References the `<button id="play-button">` element.
    - `popup`: References the `<div class="popup-container" id="popup-container">` element.
    - `notification`: References the `<div class="notification-container" id="notification-container">` element.
    - `finalMessage`: References the `<h2>` element inside the popup for win/lose messages.
    - `finalMessageRevealWord`: References the `<h3>` element inside the popup to reveal the hidden word.
    - `figureParts`: A NodeList of all elements with class "figure-part" (representing parts of the hangman figure).
    - `words`: An array of words to choose from for the game.
    - `selectedWord`: Stores the randomly selected word from the `words` array.
    - `playable`: A boolean variable controlling whether the game is playable (true) or not (false).
    - `correctLetters`: An array to store correctly guessed letters.
    - `wrongLetters`: An array to store incorrectly guessed letters.
- **Functions:**
    - `displayWord()`:
        - Updates the `wordElement` HTML content based on the `correctLetters` array.
        - If the `correctLetters` array contains all letters of the `selectedWord`, the game is won and the popup is displayed.
    - `updateWrongLettersElement()`:
        - Updates the `wrongLettersElement` HTML content based on the `wrongLetters` array.
        - Updates the visibility of hangman figure parts based on the number of incorrect guesses.
        - If the number of incorrect guesses equals the number of figure parts, the game is lost and the popup is displayed.
    - `showNotification()`:
        - Adds a class "show" to the `notification` element, displaying the message.
        - Removes the "show" class after 2 seconds, hiding the message.
- **Event Listeners:**
    - `window.addEventListener("keypress", (e) => { ... })`:
        - Listens for keypress events on the window.
        - If the game is playable and the pressed key is a letter:
            - If the letter is in the `selectedWord`:
                - If the letter is not already in `correctLetters`, adds it to the array and calls `displayWord()`.
                - Otherwise, displays the notification message.
            - Otherwise:
                - If the letter is not already in `wrongLetters`, adds it to the array and calls `updateWrongLettersElement()`.
                - Otherwise, displays the notification message.
    - `playAgainButton.addEventListener("click", () => { ... })`:
        - Listens for click events on the "Play Again" button.
        - Resets the game state:
            - Sets `playable` to true.
            - Clears both `correctLetters` and `wrongLetters` arrays.
            - Selects a new random word for `selectedWord`.
            - Calls `displayWord()` and `updateWrongLettersElement()` to reset the game UI.
            - Hides the popup by setting `popup.style.display = "none"`.
- **Initialization:**
    - Calls `displayWord()` to initially display the hidden word with empty spaces.

### style.css

- **Styling:**
    - Imports the "DotGothic16" font from Google Fonts for a retro look.
    - Sets the background color, text color, font family, and basic layout of the page.
    - Defines specific styles for different HTML elements:
        - `h1`: Main heading style with letter spacing and uppercase text.
        - `h2`, `h3`: Heading styles with letter spacing.
        - `.game-container`: Styling for the game area with padding, position, margin, height, and width.
        - `.figure-container`: Styles for the hangman figure with fill, stroke, stroke-width, and stroke-linecap.
        - `.figure-part`: Styles for individual parts of the hangman figure, initially set to `display: none`.
        - `.wrong-letters-container`: Styles for the container displaying wrong letters.
        - `.wrong-letters-container p`: Styles for the "Wrong" text within the container.
        - `.wrong-letters-container span`: Styles for individual letters displayed in the container.
        - `.word`: Styles for the word element with display, position, transform, and bottom margin.
        - `.letter`: Styles for individual letters in the word element with border-bottom, font-size, margin, and height.
        - `.popup-container`: Styles for the popup container with background color, position, display, and alignment.
        - `.popup`: Styles for the popup content with background color, border-radius, box-shadow, padding, and text-align.
        - `.popup button`: Styles for the "Play Again" button with cursor, background color, color, border, margin, padding, font-size, font-family, and border-radius.
        - `.notification-container`: Styles for the notification container with background color, padding, position, transition, and transform.
        - `.notification-container.show`: Styles for the notification container when the "show" class is applied.
        - `.notification-container p`: Styles for the text within the notification container.

This documentation provides a detailed overview of the code structure and functionality of the Wordle game. You can use this information to understand how the game works and to customize or extend its features as needed.
