# Task 1)--- Day 2: Cube Conundrum ---
**Prompt1:**
please solve the following puzzle problem.input file is attached:
You're launched high into the atmosphere! The apex of your trajectory just barely reaches the surface of a large island floating in the sky. You gently land in a fluffy pile of leaves. It's quite cold, but you don't see much snow. An Elf runs over to greet you.

The Elf explains that you've arrived at Snow Island and apologizes for the lack of snow. He'll be happy to explain the situation, but it's a bit of a walk, so you have some time. They don't get many visitors up here; would you like to play a game in the meantime?

As you walk, the Elf shows you a small bag and some cubes which are either red, green, or blue. Each time you play this game, he will hide a secret number of cubes of each color in the bag, and your goal is to figure out information about the number of cubes.

To get information, once a bag has been loaded with cubes, the Elf will reach into the bag, grab a handful of random cubes, show them to you, and then put them back in the bag. He'll do this a few times per game.

You play several games and record the information from each game (your puzzle input). Each game is listed with its ID number (like the 11 in Game 11: ...) followed by a semicolon-separated list of subsets of cubes that were revealed from the bag (like 3 red, 5 green, 4 blue).

For example, the record of a few games might look like this:

Game 1: 3 blue, 4 red; 1 red, 2 green, 6 blue; 2 green
Game 2: 1 blue, 2 green; 3 green, 4 blue, 1 red; 1 green, 1 blue
Game 3: 8 green, 6 blue, 20 red; 5 blue, 4 red, 13 green; 5 green, 1 red
Game 4: 1 green, 3 red, 6 blue; 3 green, 6 red; 3 green, 15 blue, 14 red
Game 5: 6 red, 1 blue, 3 green; 2 blue, 1 red, 2 green

In game 1, three sets of cubes are revealed from the bag (and then put back again). The first set is 3 blue cubes and 4 red cubes; the second set is 1 red cube, 2 green cubes, and 6 blue cubes; the third set is only 2 green cubes.

The Elf would first like to know which games would have been possible if the bag contained only 12 red cubes, 13 green cubes, and 14 blue cubes?

In the example above, games 1, 2, and 5 would have been possible if the bag had been loaded with that configuration. However, game 3 would have been impossible because at one point the Elf showed you 20 red cubes at once; similarly, game 4 would also have been impossible because the Elf showed you 15 blue cubes at once. If you add up the IDs of the games that would have been possible, you get 8.

Determine which games would have been possible if the bag had been loaded with only 12 red cubes, 13 green cubes, and 14 blue cub
es. What is the sum of the IDs of those games?

**Response:**
The input data consists of multiple lines, each representing a game. Each game starts with a game ID (e.g., "Game 1:") followed by a semicolon-separated list of sets of colored cubes revealed during the game (e.g., "2 red, 2 green").

To solve the problem, we need to:

1. Parse the game data to extract the number of red, green, and blue cubes shown in each subset.
2. Compare the number of cubes shown in each color to the given limits (12 red, 13 green, 14 blue).
3. Determine which games meet the conditions where no subset exceeds the cube limits.
4. Sum the game IDs of valid games.

I'll now implement the solution for this.
python
#Let's load and inspect the input file to understand its structure and content
input_file_path = '/mnt/data/input'

#Read the contents of the file
with open(input_file_path, 'r') as file:
    input_data = file.readlines()

#Show the first few lines of the input to understand its structure
input_data[:10]

Result

['Game 1: 2 red, 2 green; 1 red, 1 green, 2 blue; 3 blue, 3 red, 3 green; 1 blue, 3 green, 7 red; 5 red, 3 green, 1 blue\n',
 'Game 2: 5 green, 4 red, 7 blue; 7 red, 4 green, 4 blue; 8 green, 11 blue, 4 red; 2 red, 18 blue, 3 green; 7 red, 15 blue\n',
 'Game 3: 2 green, 4 blue; 2 red, 2 green; 6 red, 1 green; 2 red, 1 green; 2 green; 5 blue, 5 red\n',
 'Game 4: 10 red, 7 green, 10 blue; 8 red, 2 green; 9 green, 6 red, 5 blue; 8 green, 2 blue, 4 red; 5 green, 9 blue; 10 red, 1 green, 9 blue\n',
 'Game 5: 10 blue, 7 green, 2 red; 2 blue, 4 red; 2 green, 9 blue, 8 red\n',
 'Game 6: 3 green, 8 red; 1 blue, 11 red, 2 green; 2 green, 15 red, 8 blue; 13 red, 6 blue, 3 green\n',
 'Game 7: 4 green, 10 red, 7 blue; 6 red, 9 blue, 9 green; 2 red, 1 blue, 6 green\n',
 'Game 8: 1 red, 3 blue, 2 green; 7 green, 2 blue; 10 green, 1 red, 2 blue; 1 red\n',
 'Game 9: 4 red, 3 green, 11 blue; 6 red, 4 green; 15 red, 7 blue, 7 green\n',
 'Game 10: 7 red, 1 blue, 5 green; 11 red, 7 green, 1 blue; 2 green, 4 blue, 13 red\n']

The sum of the IDs of the games that would have been possible with a bag containing 12 red cubes, 13 green cubes, and 14 blue cubes is 2776.

python

import re



#Limits for red, green, and blue cubes

red_limit, green_limit, blue_limit = 12, 13, 14



#Function to parse the cube counts from each game line

def parse_game_data(game_line):

    game_id = int(re.search(r'Game (\d+)', game_line).group(1))

    game_sets = re.findall(r'(\d+) (red|green|blue)', game_line)



    # Accumulate counts per set

    max_red, max_green, max_blue = 0, 0, 0

    for count, color in game_sets:

        count = int(count)

        if color == 'red':

            max_red = max(max_red, count)

        elif color == 'green':

            max_green = max(max_green, count)

        elif color == 'blue':

            max_blue = max(max_blue, count)



    return game_id, max_red, max_green, max_blue



#Store the sum of valid game IDs

valid_game_sum = 0



#Process each line of the input

for line in input_data:

    game_id, max_red, max_green, max_blue = parse_game_data(line)

    

    # Check if the game is valid based on cube limits

    if max_red <= red_limit and max_green <= green_limit and max_blue <= blue_limit:

        valid_game_sum += game_id



valid_game_sum

Result

2776
