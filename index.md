## About Me

Completing my computer science degree at Southern New Hampshire University has given me the knowledge and skillsets that employers are looking for. I have explored a number of different software languages, operating systems, and analysis tools that make me a well-rounded candidate for employment. In addition to hard skills of coding and project development, I have worked on assignments which taught me soft skills. One example of this is a data analysis project for the Bubba Gump Shrimp Factory, where I created a report for the company’s stakeholders which analyzed their current sales across various departments (restaurants, merch, etc) and found ways for them to improve those figures in the coming years. This assignment not only taught me the use of JMP programming and of data analysis methodologies, but how to craft a proper presentation. Working on other coding projects also gave me a basic understanding of both the language and the underlying data structures involved. I have learned several database languages, have learned about Windows and Linux operating systems, and have a solid understanding of the different components of a PC. The various projects I completed were designed around tasks that would be conducted in the workplace, each providing an opportunity to not only develop the software and design skills but also written and oratory ones. Outside of the coursework, I have participated in cybersecurity CTF challenges in order to learn more about the field. This has allowed me to gain a better understanding of cybersecurity as a whole and the skills required to make a career out of it. The self-study nature of the coursework at SNHU has trained me to be disciplined and to seek out the answer from various sources whenever I have any issues. All told, the combination of soft and hard skills learned from my time at SNHU have prepared me for a career in computer science. 

There are two artifacts present in this ePortfolio, both of which demonstrates a different but important aspect of computer science. The first artifact is a local user authentication program written in Python that uses JSON to store and use data. This artifact demonstrates not only knowledge in the programming language, but also the underlying data structure and algorithms involved. The program has to not only function as intended, but should be robust enough to handle exceptions thrown at it by the user, which is demonstrated in the program. The second artifact is simple web application that takes data from a collection in MongoDB and displays it to a webpage. The use of MongoDB, Express, and Node.js allow for the user to see and interact with the database. Together these artifacts represent experience with software engineering/design, data structures and algorithms, and databases. Each artifact includes a written assessment about it, including details about the development and the challenges that were faced during its creation.

## Code Review

Below is an initial code review of the artifacts present in the portfolio before they were enhanced. It summarizes the artifacts and the work that will be done in order to enhance it.
(https://www.youtube.com/watch?v=yrI8WdJ-8lU)

## Artifact One - User Authentication Program

The artifact in this milestone is a local user authentication program. It is written for an imaginary City Zoo and is coded in Java. The program allows for a user to log in with a specific username and password, and only upon successful authentication of both items does the user gain access to the system. Additionally, only certain pieces of information are available for viewing by the user based on their role in the system. As system admin has the highest clearance and can see certain items, while the veterinarian and zookeeper can see certain other things respectively. This artifact was originally created in the 18EW2 term for the IT 145 class. 

This artifact was included for a couple of reasons. The first reason is that it is one of the first major coding projects I was able to successfully complete. This was a big step for my programming and was executed fairly well. By choosing this artifact to enhance, I would be able to remember how I had previously completed the program and be able to create similar programs in the future. This artifact showcases my knowledge not only of the Java program but of data structures as well. The use of different classes, functions, and internal loop structures is a great example of a simple yet efficient program that is commonly found in the real world. While many user authentication systems are web-based, having a local system mimics many of the same features. This makes understanding this type of program important. A second reason for choosing this artifact is that it fit nicely into the class requirements. This artifact is one of the most complete code-driven projects I’ve completed so far, so it is a great candidate for ‘converting to a new language’, which is Python in this case. The artifact was enhanced by being written in Python and by using JSON, which are both widely used and easily accessible formats for code to be written in. The implementation using these programs became easier and simpler than the Java version, making the code cleaner and more accessible. 

In order to meet the course requirements, the artifact had to successfully be converted from Java to Python. Not only was this successfully completed, but the program was enhanced to be more robust. The Python version does a better job of keeping track of the number of attempts a user makes when entering the password, and automatically exits the program if more than three attempts are made. Additionally, the user is prompted whether or not they would like to try again when an incorrect password is entered. This new and helpful feature makes the interaction better between the user and the program. The use of JSON files for reading data also enhances the artifact, as JSON is much easier to work with and scale according to new data compared with text files. The planned enhancements outlined in Milestone One have been met successfully with this milestone. 

There were a few challenges when completing this artifact enhancement. The primary struggle was with creating the login system to be as robust as possible. Simply using a singular while or for loop would not be enough to keep track of all the possible outcomes that might be encountered by the user. I had to learn to incorporate some Python-specific data structures (try and except) along with nested while loops and IF statements in order for the user to interact with the login system. This way, the user could be limited to three unsuccessful attempts, and any successful attempt did not end up causing the program to loop back to the beginning at any point. The next major struggle was using the JSON formatted file for the user credentials. I had a hard time figuring out a way to link a specific username to the corresponding password. Since both the username and password were their own key-value pairs, and both key-value pairs were part of a single object amongst an array of object, it was hard to isolate. The solution came from creating a new key-value structure with an object’s username’s value as a new key, and the same object’s password’s value as the new value. This way, both the username value and password values for a single object were linked, and could be easily accessed in the main program. The inclusion of an MD5 hash from the Java version was also implemented here, so a user could type in a normal string password, the password would be hashed, and that hashed value was compared against the value stored in the new key-value pairs created. By implementing the system in this manner, I was able to take advantage of JSON formatting for structure and simplicity while still keeping the integrity of the data. What began as a seemingly simple rewrite into Python became a more complex undertaking that ultimately was quite rewarding. I had not used JSON quite as much previously, so I had to seek a lot of help online with using and accessing data in JSON formatted files. And while I have more Python experience by comparison to Java, it had still been a while since I used it as extensively as I did for this enhancement. I do feel like I’ve learned quite a bit about both program types and how to better approach programming and data structures. 

Main Python Program
'''
//The is a local user authentication program for a zoo.
//The program has the user provide a username and password
//and checks those credentials to a file loaded in by the program.
//If the credentials match, then the relevant information is
//presented to the user based on their role.

//First some libraries are imported that help with hashing
//the password provided by the user and to work with json files

import json
import hashlib

//This opens a json file containing the available credentials and roles
//for each user
with open('./credentials.json') as f:
    data = json.load(f)


//Here we are redefining the data in the json file so that the usernames
//become keys and hashed passwords become values in a dictionary format.
//We are also creating a dictionary for the user role in order to allow 
//only certain information from being seen by the user.    

auth = {}
groups = {}
for user in data['users']:
    auth[user['username']] = {'hash' : user['hash'], 'id' : user['id']}

for role in data['roles']:
    groups[role['user_id']] = {'role' : role['role'], 'id' : role['id']}


//These functions are what the user will see upon successful login based on 
//their role. Currently is just a few sentences about the role, but can be 
//configured to have more information/menus.

def admin():
    print('Hello, System Admin!')
    print('As administrator, you have access to the zoo\'\s main computer system')
    print('This allows you to monitor users in the system and their roles.')

def veterinarian():
    print('Hello, Veterinarian!')
    print('As veterinarian, you have access to all of the animals\'\ health records')
    print('This allows you to view each animal\'\s medical history and current treatments/illnesses (if any), and to maintain a vaccination log.')

def zookeeper():
    print('Hello, Zookeeper!')
    print('As zookeeper, you have access to all of the animals\'\ information and their daily monitoring logs.')
    print('This allows you to track their feeding habits, habitat conditions, and general welfare.')


//The main function. After greeting the user, asks for username and password (non-hashed).
//Once the password is typed, it is hashed by the hexdigest function (performs MD5 hash).
//Once hashed, the hashed password is compared to those stored on file. The user is allowed
//to make three attempts to login before being booted out. After an unsuccessful attempt, the
//user is asked if they would like to try again. If they select yes, they go back to the main menu.
//If they choose not to retry, the program closes.

def zoo_authentication():
    attempts = 0
    quit = False
    while not quit:
        print('Hello, Welcome to the Zoo!')
        username = input('Enter Username: ')
        password = input('Enter Password: ')
        hash = hashlib.md5(password.encode())
        if hash.hexdigest() == auth[username]['hash']:
            print('Login Successful')
            role = groups[str(auth[username]['id'])]['role']
            if role == 'admin':
                admin()
                return 0
            elif role == 'veterinarian':
                veterinarian()
                return 0
            elif role == 'zookeeper':
                zookeeper()
                return 0
            else:
                print('Role Not Found')
        else:
            attempts = attempts + 1
            resp = None
            while (resp != 'Y' and resp != 'N') and attempts < 3:
                resp = input('Authentication Failed! Would you like to try again (Y/N)? ')
            if attempts >= 3:
                print('Too many attempts')
                quit = True
            if resp.upper() == 'N':
                quit = True

//This allows the .py function to be called from the terminal window

if __name__ == '__main__':
    zoo_authentication()
'''


Credentials JSON file contents
'''
{
  "users": [
    {
      "id": 1,
      "username": "griffin.keyes",
      "hash": "108de81c31bf9c622f76876b74e9285f",
      "password": "alphabet soup"
    },
    {
      "id": 2,
      "username": "rosario.dawson",
      "hash": "3e34baa4ee2ff767af8c120a496742b5",
      "password": "animal doctor"
    },
    {
      "id": 3,
      "username": "bernie.gorilla",
      "hash": "a584efafa8f9ea7fe5cf18442f32b07b",
      "password": "secret password"
    },
    {
      "id": 4,
      "username": "donald.monkey",
      "hash": "17b1b7d8a706696ed220bc414f729ad3",
      "password": "M0nk3y business"
    },
    {
      "id": 5,
      "username": "jerome.grizzlybear",
      "hash": "3adea92111e6307f8f2aae4721e77900",
      "password": "grizzly1234"
    },
    {
      "id": 6,
      "username": "bruce.grizzlybear",
      "hash": "0d107d09f5bbe40cade3de5c71e9e9b7",
      "password": "letmein"
    }
  ],
    "roles": [
      {
        "id": "1",
        "user_id": "1",
        "role": "zookeeper"
      },
      {
        "id": "2",
        "user_id": "2",
        "role": "admin"
      },
      {
        "id": "3",
        "user_id": "3",
        "role": "veterinarian"
      },
      {
        "id": "4",
        "user_id": "4",
        "role": "zookeeper"
      },
      {
        "id": "5",
        "user_id": "5",
        "role": "veterinarian"
      },
      {
        "id": "6",
        "user_id": "6",
        "role": "admin"
      }
    ]
}
'''
