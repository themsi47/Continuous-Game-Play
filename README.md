# Continuous Game Play Assignment - CS30
# Themsi Patel
# January 20, 2025
# A text-based adventure game with a storyline and interactive decisions.


# Import necessary modules
import random # Used for potential randomness in future enhancement

# Function Definitions
def main_menu():
    """Displays the main menu and handles user choices."""
    print("\n=== Welcome to the Realm of Eldoria ===")    # Game title and intro
    print("A land filled with adventure, treasures, and peril.")
    while True:       # Infinite loop for the main menu until user chooses to quit
        print("\n=== Main Menu ===")
        print("1. View Inventory") # Option to check collected items
        print("2. Begin Your Journey")    # Start the adventure
        print("3. Quit")    # EXit the game
        choice = input("Choose an option: ").strip().rstrip('.')  # Strip any whitespace or period

        # Handle user input and call respective functions
        if choice == "1":
            view_inventory()
        elif choice == "2":
            storyline()
        elif choice == "3":
            print("Farewell, brave traveler. Until next time!")   # Exit message
            break
        else:
            print("Invalid input. Please select a valid option.")   # Input validation

def view_inventory():
    """Displays the player's inventory."""
    print("\n=== Inventory ===")     # Title for the inventory display
    if inventory:  # If there are items in the inventory
        for item in inventory:     # Loop through and display each item
            print(f"- {item}")
    else:
        print("Your inventory is uncharted. Start your journey and find items!")  # New message when empty

def storyline():
    """Introduces the storyline and begins the adventure."""
    print("\n=== The Tale Begins ===")   # Introduction to the game story 
    print("You are a wandering adventurer seeking fame and fortune.")
    print("One day, you hear a tale of the Lost Crown of Eldoria, an artifact of immense power.")
    print("Determined to claim it, you set out on a journey filled with danger and decisions.")

    # Loop through the scenarios and handle user's choices
    for i in range(min(len(scenarios), 30)):  # Adjusted loop length to fit scenarios length
        print(f"\n=== Chapter {i + 1} ===")   # Display chapter number 
        current_event = scenarios[i]       # Get the current scenarios details 
        print(f"{current_event['description']}")   # Print the event description
        choices = current_event['choices']      # Retrience avaible choices
        print("Your options:")
        for idx, option in enumerate(choices):       # Display numbered choices
            print(f"{idx + 1}. {option['text']}")

        try:
            # User selects an action
            action = int(input("Choose your action: ").strip().rstrip('.'))
            selected_choice = choices[action - 1] # Match user's choice to available options
            print(selected_choice['outcome']) # Print the outcome of the selected action
 
             # Check if the selected choice provides an item 
            if 'item' in selected_choice:
                inventory.append(selected_choice['item'])   # Add the item to the inventory 
                print(f"You acquired a {selected_choice['item']}!")   # Notify the player
        except (ValueError, IndexError): # Handle invalid inputs
            print("That is not a valid choice. Please press 1, 2, or 3.")

        # Loop until the user presses Enter or 'q' to quit
        while True:
            next_action = input("Press Enter to continue or 'q' to quit your journey: ").lower()
            if next_action == '':
                break  # Continue to the next chapter if user presses Enter
            elif next_action == 'q':
                print("Your quest ends here, but the legend lives on.")
                return  # Stop the game immediately if the user presses 'q'
            else:
                print("Invalid input. Please press Enter to continue or 'q' to quit your journey.")
    
    # End of the game after Chapter 30
    print("\n=== The Journey Concludes ===")
    print("You have completed your quest. Whether victorious or defeated, your legacy is now written in the annals of Eldoria.")
    print("Thank you for playing!")


# Game Setup
inventory = []  # Initilize an empty inventory for the
scenarios = [   # List of scenarios with descriptions and choices
    {
        "description": "You arrive at a fork in the road.",
        "choices": [
            {"text": "Take the left path.", "outcome": "You find an abandoned campsite.", "item": "flint stone"},
            {"text": "Take the right path.", "outcome": "You are ambushed by a group of bandits!", "item": "dagger"},
            {"text": "Set up camp here.", "outcome": "You rest and recover your strength."}
        ]
    },
    {
        "description": "A mysterious traveler approaches you with a riddle.",
        "choices": [
            {"text": "Answer the riddle.", "outcome": "The traveler rewards you with a silver key.", "item": "silver key"},
            {"text": "Ignore the traveler.", "outcome": "You continue your journey in silence."},
            {"text": "Attack the traveler.", "outcome": "The traveler vanishes in a puff of smoke, leaving nothing behind."}
        ]
    },
    {
        "description": "You find a glowing chest in the middle of the forest.",
        "choices": [
            {"text": "Open the chest.", "outcome": "You find a stash of gold coins.", "item": "gold coins"},
            {"text": "Inspect the chest for traps.", "outcome": "You disarm a poison dart trap!"},
            {"text": "Walk away from the chest.", "outcome": "You decide it's not worth the risk."}
        ]
    },
    {
        "description": "A wild troll blocks your path.",
        "choices": [
            {"text": "Fight the troll.", "outcome": "You defeat the troll after a tough battle.", "item": "troll tooth"},
            {"text": "Offer the troll some food.", "outcome": "The troll lets you pass unharmed."},
            {"text": "Find another way around.", "outcome": "You manage to bypass the troll safely."}
        ]
    },
    {
        "description": "You find an ancient altar glowing with magical runes.",
        "choices": [
            {"text": "Touch the altar.", "outcome": "You are imbued with a strange energy."},
            {"text": "Read the runes.", "outcome": "You learn a new spell: Fireball.", "item": "spell scroll"},
            {"text": "Ignore the altar.", "outcome": "You move on, leaving the mystery behind."}
        ]
    },
    {
        "description": "You hear cries for help from deep within the woods.",
        "choices": [
            {"text": "Rush to help.", "outcome": "You rescue a trapped villager and gain their gratitude.", "item": "healing potion"},
            {"text": "Approach cautiously.", "outcome": "You find an injured animal, nursing it back to health."},
            {"text": "Ignore the cries.", "outcome": "You avoid potential danger but feel uneasy."}
        ]
    },
    {
        "description": "A glowing portal materializes in front of you.",
        "choices": [
            {"text": "Step through the portal.", "outcome": "You are transported to a mystical realm.", "item": "enchanted gem"},
            {"text": "Investigate the portal's edges.", "outcome": "You discover strange symbols, but their meaning eludes you."},
            {"text": "Turn away from the portal.", "outcome": "You decide to play it safe and continue your journey."}
        ]
    },
    {
        "description": "An old map lies on the ground.",
        "choices": [
            {"text": "Pick up the map.", "outcome": "The map reveals a hidden treasure location.", "item": "ancient map"},
            {"text": "Leave the map.", "outcome": "Perhaps it's best not to meddle with unknown artifacts."},
            {"text": "Destroy the map.", "outcome": "The map burns away, leaving only ashes."}
        ]
    },
    
    {"description": "A storm forces you to seek shelter in a cave.",
     "choices": [{"text": "Light a fire for warmth.", "outcome": "You find comfort but attract some animals.", "item": "torch"}, 
                 {"text": "Explore deeper into the cave.", "outcome": "You stumble upon hidden crystals.", "item": "crystals"}, 
                 {"text": "Stay near the entrance.", "outcome": "You avoid any encounters but remain cold."}]},
    
    {"description": "A mysterious voice whispers from the shadows.",
     "choices": [{"text": "Follow the voice.", "outcome": "You uncover a secret hideout.", "item": "amulet"},
                 {"text": "Shout back into the darkness.", "outcome": "The voice ceases, leaving an eerie silence."}, 
                 {"text": "Ignore it.", "outcome": "The whispers fade into nothing."}]},
    
    {"description": "You come across a wizard's tower.",
     "choices": [{"text": "Knock on the door.", "outcome": "The wizard invites you inside and offers you a magical staff.", "item": "magical staff"},
                 {"text": "Leave without speaking to the wizard.", "outcome": "You walk away, feeling a loss of opportunity."}, 
                 {"text": "Climb the tower's exterior.", "outcome": "You reach the top and discover a hidden treasure."}],
    },
    
    {"description": "A peaceful village is nestled in the hills.",
     "choices": [{"text": "Talk to the villagers.", "outcome": "They welcome you warmly and offer food and supplies.", "item": "bread basket"},
                 {"text": "Purchase goods from the market.", "outcome": "You acquire potions and herbs from the vendors."}, 
                 {"text": "Leave immediately.", "outcome": "You continue your journey without engaging with anyone."}],
    },
    
    {"description": "An abandoned library calls out to your curiosity.",
     "choices": [{"text": "Enter the library.", "outcome": "You find a forgotten tome full of ancient spells.", "item": "spell book"},
                 {"text": "Leave the library untouched.", "outcome": "You decide not to interfere with the place."}, 
                 {"text": "Investigate the surrounding area.", "outcome": "You discover hidden passages under the library."}],
    },

    {"description": "A strange figure in a cloak stops you on the path.",
     "choices": [{"text": "Ask the figure who they are.", "outcome": "The figure reveals themselves as a mystic who grants you a vision.", "item": "vision scroll"},
                 {"text": "Challenge the figure to a duel.", "outcome": "You engage in a magical duel, but the figure vanishes before a winner is declared."},
                 {"text": "Ignore the figure and continue on.", "outcome": "The figure vanishes from your sight."}]},
    
    {"description": "A battle-worn knight needs your help.",
     "choices": [{"text": "Help the knight fight the enemies.", "outcome": "Together, you defeat the invaders. The knight offers you a sword.", "item": "sword"},
                 {"text": "Offer to heal the knight.", "outcome": "You use your healing skills to mend their wounds."}, 
                 {"text": "Walk away from the knight.", "outcome": "You continue your journey without engaging."}],
    },
    
    {"description": "You stumble upon a rare flower in a hidden glade.",
     "choices": [{"text": "Pick the flower.", "outcome": "You gain an item with healing properties.", "item": "healing flower"},
                 {"text": "Take a picture of the flower.", "outcome": "You feel satisfied to document this rare sight."}, 
                 {"text": "Leave the flower be.", "outcome": "You decide to leave it undisturbed in its natural habitat."}],
    },
    
    {"description": "A dragon challenges you to a riddling contest.",
     "choices": [{"text": "Accept the challenge.", "outcome": "You solve the dragon's riddle and win a scale from its hide.", "item": "dragon scale"},
                 {"text": "Decline the challenge.", "outcome": "The dragon respects your decision and allows you to pass safely."}, 
                 {"text": "Flee the contest.", "outcome": "The dragon grows agitated but doesn't chase you."}],
    },

    {"description": "The sky turns dark as you approach a shadowy castle.",
     "choices": [{"text": "Enter the castle.", "outcome": "You enter, only to be surrounded by phantoms who offer you a cursed necklace.", "item": "cursed necklace"},
                 {"text": "Avoid the castle.", "outcome": "You pass by without any ill effects."},
                 {"text": "Search for a secret passage into the castle.", "outcome": "You discover a hidden entrance under the castle's moat."}],
    },
        {
        "description": "You come across an ancient battlefield littered with old armor and weapons.",
        "choices": [
            {"text": "Search for useful items.", "outcome": "You find a strong shield among the remains.", "item": "shield"},
            {"text": "Examine the battlefield for clues.", "outcome": "You uncover a mysterious emblem among the debris."},
            {"text": "Leave the area.", "outcome": "You feel a sense of unease and decide to move on."}
        ]
    },
    {
        "description": "A merchant offers you a peculiar item in the market.",
        "choices": [
            {"text": "Buy the item.", "outcome": "You acquire a strange artifact that radiates power.", "item": "mysterious artifact"},
            {"text": "Ask about its origins.", "outcome": "The merchant gets nervous and quickly walks away."},
            {"text": "Refuse the offer and leave.", "outcome": "You leave the market and continue on your journey."}
        ]
    },
    {
        "description": "You encounter a wild wolf pack blocking your path.",
        "choices": [
            {"text": "Fight the wolves.", "outcome": "After a fierce battle, you defeat the wolves and gain a wolf pelt.", "item": "wolf pelt"},
            {"text": "Attempt to tame one of the wolves.", "outcome": "One wolf grows curious but backs away at the last moment."},
            {"text": "Find another route around.", "outcome": "You decide to sneak past the pack without confrontation."}
        ]
    },
    {
        "description": "You find a dark, mist-covered pond in the forest.",
        "choices": [
            {"text": "Swim across the pond.", "outcome": "The mist clears momentarily, revealing a hidden cave beneath the water."},
            {"text": "Examine the mist.", "outcome": "The mist feels magical but doesn’t affect you."},
            {"text": "Leave the pond untouched.", "outcome": "You decide not to explore this strange phenomenon."}
        ]
    },
    {
        "description": "You find a journal written by an adventurer long gone.",
        "choices": [
            {"text": "Read the journal.", "outcome": "The journal hints at a powerful artifact hidden nearby.", "item": "journal"},
            {"text": "Take the journal with you.", "outcome": "You pocket the journal, hoping its clues will help you later."},
            {"text": "Leave the journal.", "outcome": "You decide to leave the adventurer's story behind."}
        ]
    },
    {
        "description": "A powerful sorceress blocks your path and demands a test of your skills.",
        "choices": [
            {"text": "Accept the challenge.", "outcome": "You pass the sorceress' test and are rewarded with a magic elixir.", "item": "magic elixir"},
            {"text": "Refuse the challenge.", "outcome": "The sorceress curses you with a minor spell that drains your energy."},
            {"text": "Try to sneak around her.", "outcome": "She catches you but allows you to pass with a warning."}
        ]
    },
    {
        "description": "A sudden earthquake shakes the ground beneath you.",
        "choices": [
            {"text": "Seek shelter under a large rock.", "outcome": "The rock provides safety, but some debris falls nearby."},
            {"text": "Try to outrun the tremors.", "outcome": "You manage to escape but suffer minor injuries."},
            {"text": "Stay still and wait for it to pass.", "outcome": "The tremors stop, but your nerves are on edge."}
        ]
    },
    {
        "description": "You find an old bell with an inscription inside an abandoned chapel.",
        "choices": [
            {"text": "Ring the bell.", "outcome": "A hidden door opens, revealing a secret room full of treasure.", "item": "treasure chest"},
            {"text": "Inspect the inscription.", "outcome": "The inscription hints at an ancient prophecy involving your fate."},
            {"text": "Leave the bell alone.", "outcome": "You decide not to disturb the ancient artifact."}
        ]
    },
    {
        "description": "A wounded animal crosses your path.",
        "choices": [
            {"text": "Help the animal.", "outcome": "You tend to the animal’s wounds and gain its trust, earning a helpful companion.", "item": "animal companion"},
            {"text": "Ignore the animal and move on.", "outcome": "You leave the animal behind, feeling a bit guilty."},
            {"text": "Put the animal out of its misery.", "outcome": "You do the humane thing, but the action haunts you."}
        ]
    },
    {
        "description": "You enter a maze of tall, twisting hedges.",
        "choices": [
            {"text": "Follow the left path.", "outcome": "You get stuck in a loop and end up back where you started."},
            {"text": "Climb over the hedges.", "outcome": "You manage to escape the maze with little effort."},
            {"text": "Walk straight ahead.", "outcome": "The path winds around, but you eventually find the exit."}
        ]
    },
    {
        "description": "An eerie laughter fills the air as you pass through a haunted forest.",
        "choices": [
            {"text": "Investigate the laughter.", "outcome": "You find a ghost trapped in the forest, offering a valuable clue.", "item": "ghost's blessing"},
            {"text": "Ignore the laughter.", "outcome": "You leave the forest, but the sound lingers in your ears."},
            {"text": "Run from the laughter.", "outcome": "You manage to escape, but the fear of the forest haunts you."}
        ]
    },
    {
        "description": "A group of friendly gnomes offers you their assistance.",
        "choices": [
            {"text": "Accept their help.", "outcome": "The gnomes give you a magical charm that protects you from danger.", "item": "gnome's charm"},
            {"text": "Decline their offer.", "outcome": "The gnomes shrug and leave, but you feel they might have been helpful."},
            {"text": "Trade with the gnomes.", "outcome": "You exchange some of your items for theirs, gaining some useful tools."}
        ]
    }
]


# Start the Game
if __name__ == "__main__":
    main_menu()      # Launch the main menu 

