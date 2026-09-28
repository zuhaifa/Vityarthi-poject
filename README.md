# Vityarthi-poject

import random
CHOICES = {"rock": "🪨", "paper": "📄", "scissors": "✂️"}
BEATS = {"rock": "scissors", "paper": "rock", "scissors": "paper"}

# Shortcuts so the player can type r / p / s
SHORTCUTS = {"r": "rock", "p": "paper", "s": "scissors"}


def get_player_choice():
    """Ask the player for a choice until a valid one is entered."""
    while True:
        raw = input("Choose rock (r), paper (p) or scissors (s): ").strip().lower()
        raw = SHORTCUTS.get(raw, raw)
        if raw in CHOICES:
            return raw
        print("❌ Invalid choice. Please try again.")


def get_computer_choice():
    """Computer picks randomly."""
    return random.choice(list(CHOICES))


def decide_winner(player, computer):
    """Return 'player', 'computer' or 'draw'."""
    if player == computer:
        return "draw"
    if BEATS[player] == computer:
        return "player"
    return "computer"


def get_number_of_rounds():
    """Ask how many rounds the player wants to play."""
    while True:
        try:
            rounds = int(input("How many rounds do you want to play? (e.g. 3, 5): "))
            if rounds > 0:
                return rounds
            print("❌ Please enter a number greater than 0.")
        except ValueError:
            print("❌ Please enter a valid number.")


def play_game():
    """Play one full game (multiple rounds) and show the final result."""
    rounds = get_number_of_rounds()
    player_score = 0
    computer_score = 0

    for round_no in range(1, rounds + 1):
        print(f"\n--- Round {round_no} of {rounds} ---")
        player = get_player_choice()
        computer = get_computer_choice()

        print(f"You chose:      {CHOICES[player]} {player}")
        print(f"Computer chose: {CHOICES[computer]} {computer}")

        result = decide_winner(player, computer)
        if result == "player":
            player_score += 1
            print("✅ You win this round!")
        elif result == "computer":
            computer_score += 1
            print("💻 Computer wins this round!")
        else:
            print("🤝 It's a draw!")

        print(f"Score -> You: {player_score} | Computer: {computer_score}")

    print("\n========== FINAL RESULT ==========")
    print(f"You: {player_score} | Computer: {computer_score}")
    if player_score > computer_score:
        print("🎉 Congratulations, you won the game!")
    elif computer_score > player_score:
        print("😢 Computer won the game. Better luck next time!")
    else:
        print("🤝 The game is a tie!")
    print("==================================")


def main():
    print("=" * 34)
    print("   ROCK  PAPER  SCISSORS GAME")
    print("=" * 34)

    while True:
        play_game()
        again = input("\nPlay again? (y/n): ").strip().lower()
        if again != "y":
            print("Thanks for playing! 👋")
            break


if __name__ == "__main__":
    main()
