```py
# 1. mario
while True:
    try:
        height = int(input("Height: "))
        if 0 < height <= 8:
            break
    except ValueError:
        print("Rejected")

# 2. cash
cents = round(change * 100)
coins = 0

coins += cents // 25
cents %= 25

# 3. credit
card = input("Number: ")
rev_card = card[::-1]

total = 0

for digit in rev_card[1::2]:
    n = int(digit) * 2
    total += (n // 10) + (n % 10)

for digit in rev_card[0::2]:
    total += int(digit)

# 4. readability
if char.isalpha():

# 5. dna
def main():

    # Check for the command line argument
    if len(sys.argv) != 3:
        print("Usage: python dna.py data.csv sequence.txt")
        sys.exit(1)

    # Read database file into a variable
    rows = []
    with open(sys.argv[1]) as file:
        reader = csv.DictReader(file)
        str_list = reader.fieldnames[1:]
        for row in reader:
            rows.append(row)


    # Read DNA sequence file into a variable
    with open(sys.argv[2]) as file:
        dna_sequence = file.read()

    # Find longest match of each STR in DNA sequence
    result = {}
    for str_name in str_list:
        result[str_name] = longest_match(dna_sequence, str_name)

    # Check database for matching profiles
    for person in rows:
        match = True
        for str_name in str_list:
            if int(person[str_name]) != result[str_name]:
                match = False
                break

        if match:
            print(person["name"])
            return

    print("No match")

    return
