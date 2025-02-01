# online-voting-system-using-python
import os

class VotingSystem:
    def _init_(self):
        self.candidates = {}
        self.votes = {}
        self.load_data()

    def load_data(self):
        # Load existing data from files (if any)
        if os.path.exists("candidates.txt"):
            with open("candidates.txt", "r") as file:
                for line in file:
                    name = line.strip()
                    self.candidates[name] = 0  # Initialize vote count

        if os.path.exists("votes.txt"):
            with open("votes.txt", "r") as file:
                for line in file:
                    voter_id, vote = line.strip().split(",")
                    self.votes[voter_id] = vote

    def save_data(self):
        # Save candidate list and vote data
        with open("candidates.txt", "w") as file:
            for candidate in self.candidates:
                file.write(candidate + "\n")

        with open("votes.txt", "w") as file:
            for voter_id, vote in self.votes.items():
                file.write(f"{voter_id},{vote}\n")

    def add_candidate(self):
        name = input("Enter candidate name: ")
        if name in self.candidates:
            print("Candidate already exists.")
        else:
            self.candidates[name] = 0
            print(f"Candidate {name} added.")

    def vote(self):
        voter_id = input("Enter your voter ID: ")
        if voter_id in self.votes:
            print("You have already voted.")
        else:
            print("Candidates are:")
            for index, candidate in enumerate(self.candidates.keys(), 1):
                print(f"{index}. {candidate}")
            choice = int(input("Choose a candidate by number: "))
            chosen_candidate = list(self.candidates.keys())[choice - 1]
            self.votes[voter_id] = chosen_candidate
            self.candidates[chosen_candidate] += 1
            print(f"Vote recorded for {chosen_candidate}.")

    def display_results(self):
        print("\nVoting Results:")
        for candidate, votes in self.candidates.items():
            print(f"{candidate}: {votes} votes")

    def start(self):
        while True:
            print("\n1. Add candidate")
            print("2. Vote")
            print("3. Display results")
            print("4. Exit")
            choice = input("Choose an option: ")
            if choice == "1":
                self.add_candidate()
            elif choice == "2":
                self.vote()
            elif choice == "3":
                self.display_results()
            elif choice == "4":
                self.save_data()
                print("Goodbye!")
                break
            else:
                print("Invalid option, please try again.")

if _name_ == "_main_":
    system = VotingSystem()
    system.start()
