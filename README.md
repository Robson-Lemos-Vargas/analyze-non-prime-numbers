# analyze-non-prime-numbers - This code may take up to 10 minutes to generate the file.
Python Code for Pattern Analysis in Non-Prime Odd Numbers
import openpyxl
from openpyxl.styles import Font, PatternFill

# Function to check if a number is prime
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

# Function to generate all odd numbers up to max_num excluding multiples of 5
def generate_odd_numbers_not_multiple_of_5(start, max_num):
    odd_numbers = []
    for num in range(start, max_num + 1, 2):  # Only odd numbers
        if num % 5 != 0:
            odd_numbers.append(num)
    return odd_numbers

# Parameters for the analysis
max_num = 1000000  # Expanded up to 1,000,000
rows = 4           # Number of rows per column (vertical)
columns = 33       # Number of columns per table

# Generate the sequence of numbers
all_sequence = generate_odd_numbers_not_multiple_of_5(11, max_num)

# Pattern of numbers to color (blue cells) - First block
coloring_pattern_first_block = [
    21, 27, 33, 39, 51, 57, 63, 69, 81, 87, 93, 99, 111, 117, 121, 123, 129, 141,
    143, 147, 153, 159, 171, 177, 183, 187, 189, 201, 207, 209, 213, 219, 231,
    237, 243, 249, 253, 261, 267, 273, 279, 291, 297, 303, 309, 319, 321, 327,
    333, 339, 77
]

# Create an Excel file
doc = openpyxl.Workbook()
sheet = doc.active
sheet.title = "Alternate Odds"

# Styles
blue_fill = PatternFill(start_color="ADD8E6", end_color="ADD8E6", fill_type="solid")  # Light blue
black_font = Font(color="000000")  # Black font
red_bold_font = Font(color="FF0000", bold=True)  # Red and bold font

# Fill the sheet with numbers distributed vertically in columns
index = 0
starting_row = 1
coloring_pattern = []  # List to store the coloring pattern of the first block

# Fill the first block and capture the pattern
for c in range(columns):  # Iterate through columns A to AG
    for l in range(rows):  # Iterate through rows 1 to 4
        if index < len(all_sequence):
            value = all_sequence[index]
            cell = sheet.cell(row=l + starting_row, column=c + 1)  # Filling cells
            cell.value = value

            # Apply formatting for prime numbers
            if is_prime(value):
                cell.font = red_bold_font  # Apply red and bold font
            else:
                cell.font = black_font  # Apply black font for non-prime numbers

            # Record coloring pattern
            if value in coloring_pattern_first_block:
                cell.fill = blue_fill
                coloring_pattern.append((l, c))  # Store the position of the colored cell

            index += 1
        else:
            break

starting_row += rows + 1  # Add 1 to skip a blank line

# Replicate the coloring pattern for subsequent blocks
while index < len(all_sequence):
    for c in range(columns):  # Iterate through columns A to AG
        for l in range(rows):  # Iterate through rows 1 to 4
            if index < len(all_sequence):
                value = all_sequence[index]
                cell = sheet.cell(row=l + starting_row, column=c + 1)  # Filling cells
                cell.value = value

                # Apply formatting for prime numbers
                if is_prime(value):
                    cell.font = red_bold_font  # Apply red and bold font
                else:
                    cell.font = black_font  # Apply black font for non-prime numbers

                # Apply coloring based on the captured pattern
                if (l, c) in coloring_pattern:
                    cell.fill = blue_fill

                index += 1
            else:
                break
    starting_row += rows + 1  # Add 1 to skip a blank line

# Adding blue coloring for Column A
row = 2  # Start from the second row
while row <= sheet.max_row:
    cell = sheet.cell(row=row, column=1)  # Only column A
    value = cell.value
    if value and (value - 341) % 330 == 0:  # Check the pattern (increments of 330)
        cell.fill = blue_fill
    row += 1

# Save the Excel file
doc.save("corrected_odds_column_a.xlsx")

print("Data has been saved to the file 'corrected_odds_column_a.xlsx'. Please note that the file generation may take up to 10 minutes.")![Image prime numbers visual pattern](https://github.com/user-attachments/assets/49f81dad-6f62-43d5-b2da-08985079ae5e)
[corrected_odds_column_a.xlsx](https://github.com/user-attachments/files/18722009/corrected_odds_column_a.xlsx)
[corrected_odds_column_a.xlsx](https://github.com/user-attachments/files/18722005/corrected_odds_column_a.xlsx)
