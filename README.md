from typing import List




stages = [
r'''
  +---+
  |   |
  O   |
 /|\  |
 / \  |
      |
=========
''',
r'''
  +---+
  |   |
  O   |
 /|\  |
 /    |
      |
=========
''',
r'''
  +---+
  |   |
  O   |
 /|\  |
      |
      |
=========
''',
r'''
  +---+
  |   |
  O   |
 /|   |
      |
      |
=========
''',
r'''
  +---+
  |   |
  O   |
  |   |
      |
      |
=========
''',
r'''
  +---+
  |   |
  O   |
      |
      |
      |
=========
''',
r'''
  +---+
  |   |
      |
      |
      |
      |
=========
'''
]

logo = '''
 _                                             
| |                                            
| |__   __ _ _ __   __ _ _ __ ___   __ _ _ __  
| '_ \\ / _` | '_ \\ / _` | '_ ` _ \\ / _` | '_ \\ 
| | | | (_| | | | | (_| | | | | | | (_| | | | |
|_| |_|\\__,_|_| |_|\\__, |_| |_| |_|\\__,_|_| |_|
                    __/ |                      
                   |___/    HANGMAN GAME
'''
import random
from Hangman_words import words_list
from Hangman_art import  logo

# Game initialization
lives = 6
print(logo)

chosen_word = "HELLO"
    #(random.choice(words_list))
# Uncomment for debugging:
# print(f"(DEBUG) The chosen word is: {chosen_word}")

word_length = len(chosen_word)
placeholder = "_" * word_length
print("Word to guess: " + placeholder)

game_over = False
correct_letters = []

while not game_over:
    print(f"\n************** {lives}/6 LIVES LEFT **************")
    guess = input("Guess a letter: ").lower()

    if guess in correct_letters:
        print(f"You've already guessed '{guess}'. Try a new letter.")
        continue  # Skip the rest of the loop and prompt again

    correct_letters.append(guess)

    display = ""
    for letter in chosen_word:
        if letter in correct_letters:
            display += letter
        else:
            display += "_"

    print("Word to guess: " + display)

    if guess not in chosen_word:
        lives -= 1
        print(f"You guessed '{guess}', which is not in the word. You lose a life.")
        print(stages[lives])  # Show hangman stage for current life

    if "_" not in display:
        game_over = True
        print("\n🎉🎉🎉 CONGRATULATIONS, YOU WIN! 🎉🎉🎉")
        print("The word was:", chosen_word)

    if lives == 0:
        game_over = True
        print("\n💀💀💀 YOU LOSE 💀💀💀")
        print(f"The word was: {chosen_word}")
        print(stages[0])
