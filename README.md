# Paasword-generator-and-password-strengthen
# ABSTRACT
In today's digital age, the increasing prevalence of cyber threats poses significant risks to personal and organizational data security. Many users still rely on weak or easily guessable passwords, making them vulnerable to data breaches and identity theft. This issue is particularly pressing for individuals without the technical expertise to create strong passwords or for those managing multiple accounts, leading to poor password practices and decreased overall security. Addressing this social problem requires a user-friendly solution that not only generates strong passwords but also educates users on best practices for online security.
# PROGRAM
```
import random

class Alphabet:
    UPPERCASE_LETTERS = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    LOWERCASE_LETTERS = "abcdefghijklmnopqrstuvwxyz"
    NUMBERS = "1234567890"
    SYMBOLS = "!@#$%^&*()-_=+\\/~?"
    
    def _init_(self, uppercase_included, lowercase_included, numbers_included, special_characters_included):
        self.pool = ""
        if uppercase_included:
            self.pool += self.UPPERCASE_LETTERS
        if lowercase_included:
            self.pool += self.LOWERCASE_LETTERS
        if numbers_included:
            self.pool += self.NUMBERS
        if special_characters_included:
            self.pool += self.SYMBOLS

    def get_alphabet(self):
        return self.pool

class Password:
    def _init_(self, value):
        self.value = value
        self.length = len(value)

    def char_type(self, c):
        if c.isupper():
            return 1  # Uppercase
        elif c.islower():
            return 2  # Lowercase
        elif c.isdigit():
            return 3  # Digit
        else:
            return 4  # Symbol

    def password_strength(self):
        used_upper = used_lower = used_num = used_sym = False
        score = 0

        for c in self.value:
            type_ = self.char_type(c)
            if type_ == 1: used_upper = True
            if type_ == 2: used_lower = True
            if type_ == 3: used_num = True
            if type_ == 4: used_sym = True

        if used_upper: score += 1
        if used_lower: score += 1
        if used_num: score += 1
        if used_sym: score += 1
        if self.length >= 8: score += 1
        if self.length >= 16: score += 1

        return score

    def calculate_score(self):
        score = self.password_strength()
        if score == 6:
            return "This is a very good password :D Check the Useful Information section to make sure it satisfies the guidelines."
        elif score >= 4:
            return "This is a good password :) but you can still do better."
        elif score >= 3:
            return "This is a medium password :/ try making it better."
        else:
            return "This is a weak password :( definitely find a new one."

    def _str_(self):
        return self.value

class Generator:
    def _init_(self):
        self.alphabet = None

    def main_loop(self):
        print("Welcome to Ziz Password Services :)")
        self.print_menu()

        user_option = "-1"

        while user_option != "4":
            user_option = input("Choice: ")

            if user_option == "1":
                self.request_password()
            elif user_option == "2":
                self.check_password()
            elif user_option == "3":
                self.print_useful_info()
            elif user_option == "4":
                self.print_quit_message()
            else:
                print("Kindly select one of the available commands")
                self.print_menu()

    def generate_password(self, length):
        pass_chars = []
        alphabet_length = len(self.alphabet.get_alphabet())

        for _ in range(length):
            index = random.randint(0, alphabet_length - 1)
            pass_chars.append(self.alphabet.get_alphabet()[index])

        return Password(''.join(pass_chars))

    def print_useful_info(self):
        print("\nUse a minimum password length of 8 or more characters if permitted")
        print("Include lowercase and uppercase alphabetic characters, numbers and symbols if permitted")
        print("Generate passwords randomly where feasible")
        print("Avoid using the same password twice (e.g., across multiple user accounts and/or software systems)")
        print("Avoid character repetition, keyboard patterns, dictionary words, letter or number sequences,")
        print("usernames, relative or pet names, romantic links (current or past) and biographical information.")
        print("Avoid using information that colleagues and/or acquaintances might know to be associated with the user.")
        print("Do not use passwords which consist wholly of any simple combination of the aforementioned weak components.")

    def request_password(self):
        include_upper = include_lower = include_num = include_sym = False
        correct_params = True

        print("\nHello, welcome to the Password Generator :) Answer the following questions by Yes or No\n")

        while correct_params:
            include_lower = self.get_inclusion("Do you want Lowercase letters \"abcd...\" to be used? ")
            include_upper = self.get_inclusion("Do you want Uppercase letters \"ABCD...\" to be used? ")
            include_num = self.get_inclusion("Do you want Numbers \"1234...\" to be used? ")
            include_sym = self.get_inclusion("Do you want Symbols \"!@#$...\" to be used? ")

            if not (include_upper or include_lower or include_num or include_sym):
                print("You have selected no characters to generate your password, at least one of your answers should be Yes\n")
                continue

            correct_params = False

        length = int(input("Great! Now enter the length of the password: "))

        self.alphabet = Alphabet(include_upper, include_lower, include_num, include_sym)
        password = self.generate_password(length)

        print("Your generated password ->", password)

    def get_inclusion(self, question):
        while True:
            response = input(question).strip().lower()
            if response in ["yes", "no"]:
                return response == "yes"
            print("You have entered something incorrect, let's go over it again.")

    def check_password(self):
        input_password = input("\nEnter your password: ")
        password = Password(input_password)
        print(password.calculate_score())

    def print_menu(self):
        print("\nEnter 1 - Password Generator")
        print("Enter 2 - Password Strength Check")
        print("Enter 3 - Useful Information")
        print("Enter 4 - Quit")


    def print_quit_message(self):
        print("Closing the program bye bye!")

if _name_ == "_main_":
    generator = Generator()
    generator.main_loop()
```
# OUTPUT
![image](https://github.com/user-attachments/assets/c4d0b3a2-6e81-4d9d-8709-04fee9984852)
