# blackjack.py
import random 
logo = """
.------.            _     _            _    _            _    
|A_  _ |.          | |   | |          | |  (_)          | |   
|( \/ ).-----.     | |__ | | __ _  ___| | ___  __ _  ___| | __
| \  /|K /\  |     | '_ \| |/ _` |/ __| |/ / |/ _` |/ __| |/ /
|  \/ | /  \ |     | |_) | | (_| | (__|   <| | (_| | (__|   < 
`-----| \  / |     |_.__/|_|\__,_|\___|_|\_\ |\__,_|\___|_|\_\\
      |  \/ K|                            _/ |                
      `------'                           |__/           
"""

                   

def deal_card():
    
    cards = [11,2,3,4,5,6,7,8,9,10,10,10,10]
    card = random.choice(cards)
    return card
# create an empty lists namely user_card and computer_card
user_card = []
computer_card = []
is_game_over = False
#create a function namely calculate_score() and move it above so that we can call it where we want
    

def calculate_score(cards):
    if sum(cards) == 21 and len(cards) == 2:
        return 0 
    if 11 in cards and sum(cards) > 21:
        cards.remove(11)
        cards.append(1)
    return sum(cards)

    #call the function deal_card() in the user_card and computer_card
def compare(user_score , computer_score):
    if user_score == computer_score:
        return "Draw"
    elif computer_score == 0:
        return "Lose , opponent got a blackjack!"
    elif user_score == 0:
        return "Win! , you got a blackjack!"
    elif user_score > 21:
        return "You lose!"
    elif computer_score > 21:
        return "You won!"
    elif user_score > computer_score:
        return "You won!"
    else:
        return "You lose!"
def play_game():
    print(logo)
    is_game_over = False
    for _ in range(2):
        user_card.append(deal_card())
        computer_card.append(deal_card())
    #create a while loop for the user
    while is_game_over is False:
        user_score = calculate_score(user_card) 
        computer_score = calculate_score(computer_card)
        print(f"Your cards: {user_card} Your score: {user_score}")
        print(f"Computer's first card: {computer_card[0]}")
        if user_score == 0 or computer_score == 0 or user_score > 21:
            is_game_over = True
        else:
            user_should_deal = input("Type 'y' to add another card , otherwise type 'n' to pass. ")
            if user_should_deal == "y":
                user_card.append(deal_card())
            else:
                is_game_over = True
    #once the user in done now create a while loop for computer:
    while computer_score != 0 and computer_score < 17:
        computer_card.append(deal_card())
        computer_score = calculate_score(computer_card)
    print(f"Your final hand: {user_card} and your final score: {user_score}")
    print(f"Computer's final hand: {computer_card} and computer's final score: {computer_score}")
    print(compare(user_score , computer_score))
    # ask the user if they want to restart the game or not:
    while input("Do you want to restart the game ? Type 'y' or 'n' ") == "y":
        play_game()

play_game()

        




