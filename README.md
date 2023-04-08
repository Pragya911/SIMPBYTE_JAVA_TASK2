# SIMPBYTE_JAVA_TASK2
this is my task 2 of my internship in simplbyte which was on to create a hangman game
import java.util.Scanner;
public class hangmani_game {
    public static void main(String[] args) {
            String[] words = {"java", "python", "javascript", "ruby", "php"}; // list of words to guess
            String wordToGuess = words[(int) (Math.random() * words.length)]; // randomly select a word from the list
            int remainingGuesses = 6; // number of guesses remaining
            boolean[] lettersGuessed = new boolean[26]; // track which letters have been guessed
            Scanner inputScanner = new Scanner(System.in); // create a scanner to read user input

            // initialize the display word with dashes
            char[] displayWord = new char[wordToGuess.length()];
            for (int i = 0; i < displayWord.length; i++) {
                displayWord[i] = '-';
            }

            // main game loop
            while (remainingGuesses > 0 && new String(displayWord).indexOf('-') != -1) {
                System.out.println("Guesses remaining: " + remainingGuesses);
                System.out.println("Word: " + new String(displayWord));
                System.out.print("Guess a letter: ");
                String input = inputScanner.nextLine().toLowerCase();

                // check if the input is a valid letter
                if (input.length() != 1 || !Character.isLetter(input.charAt(0))) {
                    System.out.println("Invalid input. Please enter a single letter.");
                    continue;
                }

                char letter = input.charAt(0);

                // check if the letter has already been guessed
                if (lettersGuessed[letter - 'a']) {
                    System.out.println("You've already guessed that letter. Try again.");
                    continue;
                }

                lettersGuessed[letter - 'a'] = true; // mark the letter as guessed

                // check if the letter is in the word
                boolean foundLetter = false;
                for (int i = 0; i < wordToGuess.length(); i++) {
                    if (wordToGuess.charAt(i) == letter) {
                        displayWord[i] = letter;
                        foundLetter = true;
                    }
                }

                if (foundLetter) {
                    System.out.println("Correct!");
                } else {
                    System.out.println("Incorrect!");
                    remainingGuesses--;
                }
            }

            if (remainingGuesses == 0) {
                System.out.println("You lose. The word was " + wordToGuess);
            } else {
                System.out.println("You win!");
            }

            inputScanner.close();
        }
    }


