# Task 1)--- Day 2: Cube Conundrum ---
**Prompt 1:**
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

**ChatGPT said:**
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

**Prompt 2:** now please solve the advanced version of this puzzle,input file is same as above:The Elf says they've stopped producing snow because they aren't getting any water! He isn't sure why the water stopped; however, he can show you how to get to the water source to check it out for yourself. It's just up ahead!

As you continue your walk, the Elf poses a second question: in each game you played, what is the fewest number of cubes of each color that could have been in the bag to make the game possible?

Again consider the example games from earlier:

Game 1: 3 blue, 4 red; 1 red, 2 green, 6 blue; 2 green
Game 2: 1 blue, 2 green; 3 green, 4 blue, 1 red; 1 green, 1 blue
Game 3: 8 green, 6 blue, 20 red; 5 blue, 4 red, 13 green; 5 green, 1 red
Game 4: 1 green, 3 red, 6 blue; 3 green, 6 red; 3 green, 15 blue, 14 red
Game 5: 6 red, 1 blue, 3 green; 2 blue, 1 red, 2 green

    In game 1, the game could have been played with as few as 4 red, 2 green, and 6 blue cubes. If any color had even one fewer cube, the game would have been impossible.
    Game 2 could have been played with a minimum of 1 red, 3 green, and 4 blue cubes.
    Game 3 must have been played with at least 20 red, 13 green, and 6 blue cubes.
    Game 4 required at least 14 red, 3 green, and 15 blue cubes.
    Game 5 needed no fewer than 6 red, 3 green, and 2 blue cubes in the bag.

The power of a set of cubes is equal to the numbers of red, green, and blue cubes multiplied together. The power of the minimum set of cubes in game 1 is 48. In games 2-5 it was 12, 1560, 630, and 36, respectively. Adding up these five powers produces the sum 2286.

For each game, find the minimum set of cubes that must have been present. What is t
he sum of the power of these sets?
**ChatGPT said:**
To solve this advanced version of the puzzle, we need to determine the minimum number of red, green, and blue cubes that must have been in the bag for each game. The steps are as follows:

    Parse each game as before to extract the counts of red, green, and blue cubes revealed in each subset.
    For each game, determine the maximum number of red, green, and blue cubes shown in any subset. This represents the minimum number of cubes needed in the bag for that game to be possible.
    Compute the power of the set of cubes for each game, which is the product of the minimum number of red, green, and blue cubes required.
    Sum the powers for all games.

I'll now implement the solution to find the sum of the powers for all games.

python
Always show details

#Function to compute the power of a game (product of the minimum red, green, and blue cubes needed)

def compute_game_power(game_line):

    game_id = int(re.search(r'Game (\d+)', game_line).group(1))

    game_sets = re.findall(r'(\d+) (red|green|blue)', game_line)



    #Track the maximum cubes needed for each color (i.e., the minimum required to make the game possible)

    max_red, max_green, max_blue = 0, 0, 0

    for count, color in game_sets:

        count = int(count)

        if color == 'red':

            max_red = max(max_red, count)

        elif color == 'green':

            max_green = max(max_green, count)

        elif color == 'blue':

            max_blue = max(max_blue, count)



    #Compute the power of the game (product of max red, green, and blue)

    power = max_red * max_green * max_blue

    return power



#Sum the powers of all games

total_power_sum = 0



#Process each line of the input to compute the total power

for line in input_data:

    total_power_sum += compute_game_power(line)



total_power_sum

Result

68638

The sum of the power of the minimum sets of cubes for all games is 68,638. ​

​
# Task 2) --- Day 1: Trebuchet?! ---
**Prompt 1:**
please solve the below puzzle probmem:Something is wrong with global snow production, and you've been selected to take a look. The Elves have even given you a map; on it, they've used stars to mark the top fifty locations that are likely to be having problems.
You've been doing this long enough to know that to restore snow operations, you need to check all fifty stars by December 25th.
Collect stars by solving puzzles. Two puzzles will be made available on each day in the Advent calendar; the second puzzle is unlocked when you complete the first. Each puzzle grants one star. Good luck!
You try to ask why they can't just use a weather machine ("not powerful enough") and where they're even sending you ("the sky") and why your map looks mostly blank ("you sure ask a lot of questions") and hang on did you just say the sky ("of course, where do you think snow comes from") when you realize that the Elves are already loading you into a trebuchet ("please hold still, we need to strap you in").
As they're making the final adjustments, they discover that their calibration document (your puzzle input) has been amended by a very young Elf who was apparently just excited to show off her art skills. Consequently, the Elves are having trouble reading the values on the document.
The newly-improved calibration document consists of lines of text; each line originally contained a specific calibration value that the Elves now need to recover. On each line, the calibration value can be found by combining the first digit and the last digit (in that order) to form a single two-digit number.
For example:
1abc2
pqr3stu8vwx
a1b2c3d4e5f
treb7uchet
**Response by Gemini 1.5 pro:**
In this example, the calibration values of these four lines are 12, 38, 15, and 77. Adding these together produces 142.
Consider your entire calibration document. What is the sum of all of the calibration values?
Here's a Python function that solves this problem, along with an explanation of the approach:

```python
import re

def sum_calibration_values(calibration_document):
   """Calculates the sum of calibration values from a document.

   Args:
       calibration_document: A string representing the calibration document, 
                            with each line separated by a newline character.

   Returns:
       The sum of all calibration values.
   """

   total_sum = 0
   for line in calibration_document.splitlines():
       digits = re.findall(r'\d', line) # Extract all digits using regular expressions
       if digits:
           calibration_value = int(digits[0] + digits[-1]) # Combine the first and last digits
           total_sum += calibration_value
   return total_sum



# Example usage (replace with your actual input):
calibration_document = """1abc2
pqr3stu8vwx
a1b2c3d4e5f
treb7uchet"""

sum_of_values = sum_calibration_values(calibration_document)
print(sum_of_values) # Output: 142


# To use with a file:
with open("your_input_file.txt", "r") as f:
   calibration_document = f.read()
   sum_of_values = sum_calibration_values(calibration_document)
   print(sum_of_values)
```

** Explanation: **

1. ** Import `re`:** This line imports the regular expression module, which is used to efficiently extract digits from each line.

2. ** `sum_calibration_values(calibration_document)` function:**
  - Initializes `total_sum` to 0.
  - Splits the input `calibration_document` into individual lines using `splitlines()`.
  - Iterates through each `line`.
  - **`re.findall(r'\d', line)`:** This is the key part. It uses a regular expression `\d` (which matches any digit) to find all digits in the current line and returns them as a list.
  - ** `if digits:`:** Checks if any digits were found in the line. This handles cases where a line might be empty or contain no digits.
  - ** `calibration_value = int(digits[0] + digits[-1])`:** Takes the first digit (`digits[0]`) and the last digit (`digits[-1]`) from the list, concatenates them into a string, and converts the result to an integer.
  - Adds the `calibration_value` to the `total_sum`.
  - Returns the final `total_sum`.

3. ** Example Usage/File Input:** The code shows how to use the function with both a sample string and how to read the input from a file named "your_input_file.txt". Make sure to replace `"your_input_file.txt"` with the actual path to your input file.



This approach is clear, concise, and handles potential edge cases (lines with no digits). Using regular expressions makes the digit extraction very efficient. Remember to replace the example input with your actual puzzle input to get the correct answer.

**Prompt 2:** now solve the second part:
Your calculation isn't quite right. It looks like some of the digits are actually spelled out with letters: one, two, three, four, five, six, seven, eight, and nine also count as valid "digits".
Equipped with this new information, you now need to find the real first and last digit on each line. For example:
two1nine
eightwothree
abcone2threexyz
xtwone3four
4nineeightseven2
zoneight234
7pqrstsixteen
In this example, the calibration values are 29, 83, 13, 24, 42, 14, and 76. Adding these together produces 281.
What is the sum of all of the calibration values?
**Response by Gemini 1.5 pro:**
```python
import re

def sum_calibration_values_part2(calibration_document):
    """Calculates the sum of calibration values, including spelled-out digits.

    Args:
        calibration_document: The calibration document string.

    Returns:
        The sum of all calibration values.
    """

    digit_map = {
        "one": "1", "two": "2", "three": "3", "four": "4", "five": "5",
        "six": "6", "seven": "7", "eight": "8", "nine": "9"
    }

    total_sum = 0
    for line in calibration_document.splitlines():
        # Use regex with overlapping matches and lookahead assertions
        all_digits = re.findall(r"(?=(\d|one|two|three|four|five|six|seven|eight|nine))", line)

        if all_digits:
            first_digit = all_digits[0]
            last_digit = all_digits[-1]

            # Convert spelled-out digits to numeric
            if first_digit in digit_map:
                first_digit = digit_map[first_digit]
            if last_digit in digit_map:
                last_digit = digit_map[last_digit]
                
            calibration_value = int(first_digit + last_digit)
            total_sum += calibration_value

    return total_sum


# Example usage (replace with your actual input):
calibration_document = """two1nine
eightwothree
abcone2threexyz
xtwone3four
4nineeightseven2
zoneight234
7pqrstsixteen"""

sum_of_values = sum_calibration_values_part2(calibration_document)
print(sum_of_values)  # Output: 281



# To use with a file:
with open("your_input_file.txt", "r") as f:
    calibration_document = f.read()
    sum_of_values = sum_calibration_values_part2(calibration_document)
    print(sum_of_values)

```


** Explanation of Changes for Part 2:**

1. ** `digit_map` Dictionary:** This dictionary maps the spelled-out digit names to their numeric equivalents.

2. ** Overlapping Matches with Lookahead Assertions:** The most crucial change is in the regular expression: `r"(?=(\d|one|two|three|four|five|six|seven|eight|nine))"`.
   - `(?= ... )` is a *lookahead assertion*. It checks if the pattern inside the parentheses matches at the current position *without* consuming any characters. This is essential for handling overlapping matches (e.g., "twone" needs to match both "two" and "one").
   - `(\d|one|two|...)` is a capturing group that matches either a digit (`\d`) or one of the spelled-out digit names.

3. ** Spelled-out Digit Conversion:** After extracting `first_digit` and `last_digit`, the code checks if they are present in the `digit_map`. If so, it replaces the spelled-out name with the corresponding number.



This improved version correctly handles the overlapping spelled-out digits and provides the accurate sum for Part 2 of the puzzle.  Remember to replace the example input and `"your_input_file.txt"` with your actual puzzle input and file path.



