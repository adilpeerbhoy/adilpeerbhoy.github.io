## About Me

Completing my computer science degree at Southern New Hampshire University has given me the knowledge and skillsets that employers are looking for. I have explored a number of different software languages, operating systems, and analysis tools that make me a well-rounded candidate for employment. In addition to hard skills of coding and project development, I have worked on assignments which taught me soft skills. One example of this is a data analysis project for the Bubba Gump Shrimp Factory, where I created a report for the company’s stakeholders which analyzed their current sales across various departments (restaurants, merch, etc) and found ways for them to improve those figures in the coming years. This assignment not only taught me the use of JMP programming and of data analysis methodologies, but how to craft a proper presentation. Working on other coding projects also gave me a basic understanding of both the language and the underlying data structures involved. I have learned several database languages, have learned about Windows and Linux operating systems, and have a solid understanding of the different components of a PC. The various projects I completed were designed around tasks that would be conducted in the workplace, each providing an opportunity to not only develop the software and design skills but also written and oratory ones. Outside of the coursework, I have participated in cybersecurity CTF challenges in order to learn more about the field. This has allowed me to gain a better understanding of cybersecurity as a whole and the skills required to make a career out of it. The self-study nature of the coursework at SNHU has trained me to be disciplined and to seek out the answer from various sources whenever I have any issues. All told, the combination of soft and hard skills learned from my time at SNHU have prepared me for a career in computer science. 

There are two artifacts present in this ePortfolio, both of which demonstrates a different but important aspect of computer science. The first artifact is a local user authentication program written in Python that uses JSON to store and use data. This artifact demonstrates not only knowledge in the programming language, but also the underlying data structure and algorithms involved. The program has to not only function as intended, but should be robust enough to handle exceptions thrown at it by the user, which is demonstrated in the program. The second artifact is simple web application that takes data from a collection in MongoDB and displays it to a webpage. The use of MongoDB, Express, and Node.js allow for the user to see and interact with the database. Together these artifacts represent experience with software engineering/design, data structures and algorithms, and databases. Each artifact includes a written assessment about it, including details about the development and the challenges that were faced during its creation.

## Code Review

Below is an initial code review of the artifacts present in the portfolio before they were enhanced. It summarizes the artifacts and the work that will be done in order to enhance it.
(https://www.youtube.com/watch?v=yrI8WdJ-8lU)

## Artifact One - User Authentication Program (First Enhancement)

This artifact underwent two enhancements, one which changed the original program language and the other which added complexity. They are here one after the other.

The artifact in this milestone is a local user authentication program. It is written for an imaginary City Zoo and is coded in Java. The program allows for a user to log in with a specific username and password, and only upon successful authentication of both items does the user gain access to the system. Additionally, only certain pieces of information are available for viewing by the user based on their role in the system. As system admin has the highest clearance and can see certain items, while the veterinarian and zookeeper can see certain other things respectively. This artifact was originally created in the 18EW2 term for the IT 145 class. 

This artifact was included for a couple of reasons. The first reason is that it is one of the first major coding projects I was able to successfully complete. This was a big step for my programming and was executed fairly well. By choosing this artifact to enhance, I would be able to remember how I had previously completed the program and be able to create similar programs in the future. This artifact showcases my knowledge not only of the Java program but of data structures as well. The use of different classes, functions, and internal loop structures is a great example of a simple yet efficient program that is commonly found in the real world. While many user authentication systems are web-based, having a local system mimics many of the same features. This makes understanding this type of program important. A second reason for choosing this artifact is that it fit nicely into the class requirements. This artifact is one of the most complete code-driven projects I’ve completed so far, so it is a great candidate for ‘converting to a new language’, which is Python in this case. The artifact was enhanced by being written in Python and by using JSON, which are both widely used and easily accessible formats for code to be written in. The implementation using these programs became easier and simpler than the Java version, making the code cleaner and more accessible. 

In order to meet the course requirements, the artifact had to successfully be converted from Java to Python. Not only was this successfully completed, but the program was enhanced to be more robust. The Python version does a better job of keeping track of the number of attempts a user makes when entering the password, and automatically exits the program if more than three attempts are made. Additionally, the user is prompted whether or not they would like to try again when an incorrect password is entered. This new and helpful feature makes the interaction better between the user and the program. The use of JSON files for reading data also enhances the artifact, as JSON is much easier to work with and scale according to new data compared with text files. The planned enhancements outlined in Milestone One have been met successfully with this milestone. 

There were a few challenges when completing this artifact enhancement. The primary struggle was with creating the login system to be as robust as possible. Simply using a singular while or for loop would not be enough to keep track of all the possible outcomes that might be encountered by the user. I had to learn to incorporate some Python-specific data structures (try and except) along with nested while loops and IF statements in order for the user to interact with the login system. This way, the user could be limited to three unsuccessful attempts, and any successful attempt did not end up causing the program to loop back to the beginning at any point. The next major struggle was using the JSON formatted file for the user credentials. I had a hard time figuring out a way to link a specific username to the corresponding password. Since both the username and password were their own key-value pairs, and both key-value pairs were part of a single object amongst an array of object, it was hard to isolate. The solution came from creating a new key-value structure with an object’s username’s value as a new key, and the same object’s password’s value as the new value. This way, both the username value and password values for a single object were linked, and could be easily accessed in the main program. The inclusion of an MD5 hash from the Java version was also implemented here, so a user could type in a normal string password, the password would be hashed, and that hashed value was compared against the value stored in the new key-value pairs created. By implementing the system in this manner, I was able to take advantage of JSON formatting for structure and simplicity while still keeping the integrity of the data. What began as a seemingly simple rewrite into Python became a more complex undertaking that ultimately was quite rewarding. I had not used JSON quite as much previously, so I had to seek a lot of help online with using and accessing data in JSON formatted files. And while I have more Python experience by comparison to Java, it had still been a while since I used it as extensively as I did for this enhancement. I do feel like I’ve learned quite a bit about both program types and how to better approach programming and data structures. 

Main Python Program
```
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
```


Credentials JSON file contents
```
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
```

## Artifact One - User Authentication Program (Second Enhancement)

The artifact in this milestone is a local user authentication program. It is written for an imaginary City Zoo and is coded in Java originally (in Python after the first enhancement as part of Milestone Two). The program allows for a user to log in with a specific username and password, and only upon successful authentication of both items does the user gain access to the system. Additionally, only certain pieces of information are available for viewing by the user based on their role in the system. As system admin has the highest clearance and can see certain items, while the veterinarian and zookeeper can see certain other things respectively. This artifact was originally created in the 18EW2 term for the IT 145 class. 

This artifact was included for a couple of reasons. The first reason is that I had recently enhanced this artifact in the previous milestone. I didn’t just want to leave it the way it was, and if there was a way to enhance it further by making it more efficient or adding complexity then it would be an even better program to showcase my abilities. As the ultimate goal of the class is to create an ePortfolio, the better my work is, the better it will showcase on the portfolio to potential employers and/or recruiters. This artifact showcases my knowledge not only of the Python program but of data structures as well. The use of different functions and internal loop structures is a great example of a simple yet efficient program that is commonly found in the real world. While many user authentication systems are web-based, having a local system mimics many of the same features. This makes understanding this type of program important. A second reason for choosing this artifact is that it fit nicely into the class requirements. This artifact is one of the most complete code-driven projects I’ve completed so far, so it is a great candidate for ‘expanding complexity’.

In order to meet the course requirements, the artifact had to be more useful than the original enhancement. In both the original Java version and the enhanced Python one, once the user successfully logs into the system, there is little for the user to do. A simple message is displayed to the user describing what types of information that user has access to, and what they might be able to do once logged in. However, nothing of that sort was included. In order to expand on the program’s complexity, I had to create new data and files for each user to interact with. The system administrator had to be able to see all the staff members, for example. The vet and zookeepers needed to see information on the animals in the zoo, which required this data to first be created and then made accessible to these users. Since the users would also like to be able to perform more than a single action once logged in, they needed to be able to choose from a menu of options and be able to return to that menu after completing that task. Last, the user had to be able to logout and return to the main login page for the zoo system. Adding all three of these components (new data, user access to data, and inclusion of menu system prompts) all make the program more robust and useful. The planned enhancements outlined in Milestone One have been met successfully with this milestone.

There were a few challenges when completing this artifact enhancement. The first item that was coded for increased complexity was the creation of new data entries for the users to access. This meant creating four new JSON formatted files – staff, animals, medical, and logs. The staff file was a rehash of the original credentials file used in the main authentication system, but without password information and an added staff_id field. The animals file contained names and animal-types for all the animals that would be used in the system (11 animals total). Each have a unique animal_id, which is used in both the medical and logs files to reference this animals’ file. The medial file contains a short medical history, illness, treatment, and vaccination log for each animal. The logs file contains habitat condition, food preference, and general welfare for each animal. Configuring each of these files was made easy by using online JSON generators to convert text to JSON format. The next item was creating a menu to access the content for each user. Since I have previous experience in creating a simple menu, the implementation in this case was not difficult. Each user is prompted to choose an option on a menu, one of which is the option to logout of the program. If a user enters a value outside those designated in the menu, or if a string is entered, the user is prompted to try again (no attempt restrictions). This used the try/except structure along with while loops and if statements in order to make the menu robust. The last part was the most difficult, which was getting the data read in by the program. Similar to the main authentication program, each of the objects in the JSON files I was working with contained multiple key-value pairs for every object. While I was able to get all the objects printed at once, I was unable to get specific objects to display based upon certain criteria. If a user wanted to just see the medical record for one animal as an example, I wasn’t able to make that happen. As it stands, each user can see all the data that they have access to, but no way to filter the results. The previous implementation of JSON files, where new dictionaries of key-value pairs are created, did not work in this situation. Not only was more information involved, but the entire object’s key-value pairs needed to be printed to the screen, not just one or two of them. Adding this level of complexity would certainly make the program even better and more useful, but I was unable to complete this at the current time. I do plan to work on this on my own outside of the course in order to improve my own skills and knowledge. While I had learned a fair amount about JSON from the last enhancement, it was not quite enough here to make the program the best it could be. Working on this enhancement showed me how complex these types of systems can be, and allowed me to gain a greater appreciation of them. While I was unable to make the full implementations, I still did learn quite a bit about JSON anyway, which will only serve me well in my career.  

Main Python Program
```
'''
The is a local user authentication program for a zoo.
The program has the user provide a username and password
and checks those credentials to a file loaded in by the program.
If the credentials match, then the relevant information is
presented to the user based on their role.

First some libraries are imported that help with hashing
the password provided by the user and to work with json files
'''
import json
import hashlib

# This opens a json file containing the available credentials and roles
# for each user
with open('./credentials.json') as f:
    data = json.load(f)

'''
Here we are redefining the data in the json file so that the usernames
become keys and hashed passwords become values in a dictionary format.
We are also creating a dictionary for the user role in order to allow 
only certain information from being seen by the user.    
'''
auth = {}
groups = {}
for user in data['users']:
    auth[user['username']] = {'hash' : user['hash'], 'id' : user['id']}

for role in data['roles']:
    groups[role['user_id']] = {'role' : role['role'], 'id' : role['id']}

'''
These functions are what the user will see upon successful login based on 
their role. The user will be able to make a choice from a menu of options.
These include viewing all the data available to them and logging out to the 
main menu. More features can be added based on the type of information
each user would like to access most often. Data is stored in json files outside
the main program and are opened within their respective functions.
'''
def admin():
    print()
    print('Hello, System Admin!')
    print('As administrator, you have access to the zoo\'\s main computer system')
    print('This allows you to monitor users in the system and their roles.')
    print()
    print('1 - View Entire Staff')
    print('2 - Logout')
    print()

    with open('./staff.json') as f:
        data = json.load(f)

    while True:
        try:
            admin_select = int(input('Please select an option to continue (1-2): '))
            if admin_select == 1:
                print(json.dumps(data['staff'], indent=2))
                anykey=input("Enter anything to return to main menu")
                admin()
            if admin_select == 2:
                print()
                print()
                zoo_authentication()
        except ValueError:
            print("Invalid choice. Enter 1-2")
    exit

def veterinarian():
    print()
    print('Hello, Veterinarian!')
    print('As veterinarian, you have access to all of the animals\'\ health records')
    print('This allows you to view each animal\'\s medical history and current treatments/illnesses (if any), and to maintain a vaccination log.')
    print()
    print('1 - View all Animals')
    print('2 - View all Medical Reports')
    print('3 - Logout')
    print()

    with open('./animals.json') as f:
        animals = json.load(f)

    with open('./medical.json') as file:
        medicals = json.load(file)

    while True:
        try:
            vet_select = int(input('Please select an option to continue (1-3): '))
            if vet_select == 1:
                print(json.dumps(animals['animal'], indent=2))
                anykey=input("Enter anything to return to main menu")
                veterinarian()
            if vet_select == 2:
                print(json.dumps(medicals['record'], indent=2))
                anykey=input("Enter anything to return to main menu")
                veterinarian()
            if vet_select == 3:
                print()
                print()
                zoo_authentication()
        except ValueError:
            print("Invalid choice. Enter 1-3")
    exit

def zookeeper():
    print('Hello, Zookeeper!')
    print('As zookeeper, you have access to all of the animals\'\ information and their daily monitoring logs.')
    print('This allows you to track their feeding habits, habitat conditions, and general welfare.')
    print()
    print('1 - View all Animals')
    print('2 - View Monitoring Logs')
    print('3 - Logout')
    print()

    with open('./animals.json') as f:
        animals = json.load(f)
    
    with open('./logs.json') as file2:
        logs = json.load(file2)

    while True:
        try:
            zoo_select = int(input('Please select an option to continue (1-3): '))
            if zoo_select == 1:
                print(json.dumps(animals['animal'], indent=2))
                anykey=input("Enter anything to return to main menu")
                zookeeper()
            if zoo_select == 2:
                print(json.dumps(logs['log'], indent=2))
                anykey=input("Enter anything to return to main menu")
                zookeeper()
            if zoo_select == 3:
                print()
                print()
                zoo_authentication()
        except ValueError:
            print("Invalid choice. Enter 1-3")
    exit

'''
The main function. After greeting the user, asks for username and password (non-hashed).
Once the password is typed, it is hashed by the hexdigest function (performs MD5 hash).
Once hashed, the hashed password is compared to those stored on file. The user is allowed
to make three attempts to login before being booted out. After an unsuccessful attempt, the
user is asked if they would like to try again. If they select yes, they go back to the main menu.
If they choose not to retry, the program closes.
 '''
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
                #return 0
            elif role == 'veterinarian':
                veterinarian()
                #return 0
            elif role == 'zookeeper':
                zookeeper()
                #return 0
            else:
                print('Role Not Found')
        else:
            attempts = attempts + 1
            resp = None
            while (resp != 'Y' and resp != 'N') and attempts < 3:
                resp = input('Authentication Failed! Would you like to try again (Y/N)? ')
            if attempts >= 3:
                print('Too many attempts - Goodbye')
                quit = True
            if resp.upper() == 'N':
                quit = True

# This allows the .py function to be called from the terminal window

if __name__ == '__main__':
    zoo_authentication()
```

Staff JSON File
```
{
  "staff": [
    {
      "id": "1",
      "staff_id": "101",
      "first_name": "Griffin",
      "last_name": "Keyes",
      "role": "zookeeper"
    },
    {
      "id": "2",
      "staff_id": "102",
      "first_name": "Rosario",
      "last_name": "Dawson",
      "role": "admin"
    },
    {
      "id": "3",
      "staff_id": "103",
      "first_name": "Bernie",
      "last_name": "Gorilla",
      "role": "veterinarian"
    },
    {
      "id": "4",
      "staff_id": "104",
      "first_name": "Donald",
      "last_name": "Monkey",
      "role": "zookeeper"
    },
    {
      "id": "5",
      "staff_id": "105",
      "first_name": "Jerome",
      "last_name": "Grizzlybear",
      "role": "veterinarian"
    },
    {
      "id": "6",
      "staff_id": "106",
      "first_name": "Bruce",
      "last_name": "Grizzlybear",
      "role": "admin"
    }
  ]
}
```
Animals JSON File
```
{
  "animal": [
    {
      "id": "1",
      "animal_id": "1",
      "first_name": "Alex",
      "type": "lion"
    },
    {
      "id": "2",
      "animal_id": "2",
      "first_name": "Marty",
      "type": "zebra"
    },
    {
      "id": "3",
      "animal_id": "3",
      "first_name": "Gloria",
      "type": "hippo"
    },
    {
      "id": "4",
      "animal_id": "4",
      "first_name": "Melman",
      "type": "giraffe"
    },
    {
      "id": "5",
      "animal_id": "5",
      "first_name": "Skipper",
      "type": "penguin"
    },
    {
      "id": "6",
      "animal_id": "6",
      "first_name": "Kowalski",
      "type": "penguin"
    },
    {
      "id": "7",
      "animal_id": "7",
      "first_name": "Rico",
      "type": "penguin"
    },
    {
      "id": "8",
      "animal_id": "8",
      "first_name": "Private",
      "type": "penguin"
    },
    {
      "id": "9",
      "animal_id": "9",
      "first_name": "Julian",
      "type": "lemur"
    },
    {
      "id": "10",
      "animal_id": "10",
      "first_name": "Maurice",
      "type": "lemur"
    },
    {
      "id": "11",
      "animal_id": "11",
      "first_name": "Mort",
      "type": "lemur"
    }
  ]
}
```
Medical Records JSON File
```
{
  "record": [
    {
      "id": "1",
      "animal_id": "1",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "egoism",
      "treatment": "none available",
      "vaccination_log": [
        "06/2020",
        "10/2018",
        "02/2017"
      ]
    },
    {
      "id": "2",
      "animal_id": "2",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "naivety",
      "treatment": "none available",
      "vaccination_log": [
        "03/2020",
        "12/2019",
        "04/2017"
      ]
    },
    {
      "id": "3",
      "animal_id": "3",
      "history": {
        "gender": "female",
        "health": "good",
        "allergies": "none"
      },
      "illness": "none",
      "treatment": "N/A",
      "vaccination_log": [
        "06/2019",
        "11/2018",
        "07/2017"
      ]
    },
    {
      "id": "4",
      "animal_id": "4",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "many"
      },
      "illness": "paranoia",
      "treatment": "none available",
      "vaccination_log": [
        "05/2020",
        "4/2019",
        "02/2018"
      ]
    },
    {
      "id": "5",
      "animal_id": "5",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "N/A",
      "treatment": "N/A",
      "vaccination_log": [
        "05/2020",
        "04/2019",
        "06/2018"
      ]
    },
    {
      "id": "6",
      "animal_id": "6",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "N/A",
      "treatment": "N/A",
      "vaccination_log": [
        "05/2020",
        "04/2019",
        "06/2018"
      ]
    },
    {
      "id": "7",
      "animal_id": "7",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "N/A",
      "treatment": "N/A",
      "vaccination_log": [
        "05/2020",
        "04/2019",
        "06/2018"
      ]
    },
    {
      "id": "8",
      "animal_id": "8",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "N/A",
      "treatment": "N/A",
      "vaccination_log": [
        "05/2020",
        "04/2019",
        "06/2018"
      ]
    },
    {
      "id": "9",
      "animal_id": "9",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "egoism",
      "treatment": "none available",
      "vaccination_log": [
        "08/2020",
        "06/2018",
        "01/2016"
      ]
    },
    {
      "id": "10",
      "animal_id": "10",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "N/A",
      "treatment": "N/A",
      "vaccination_log": [
        "12/2019",
        "04/2018",
        "06/2017"
      ]
    },
    {
      "id": "11",
      "animal_id": "11",
      "history": {
        "gender": "male",
        "health": "good",
        "allergies": "none"
      },
      "illness": "N/A",
      "treatment": "N/A",
      "vaccination_log": [
        "05/2020",
        "04/2019",
        "06/2018"
      ]
    }
  ]
}
```
Maintenance Logs File
```
{
  "log": [
    {
      "id": "1",
      "animal_id": "1",
      "food": "raw steak",
      "habitat_condition": "good",
      "welfare": "happy"
    },
    {
      "id": "2",
      "animal_id": "2",
      "food": "grass bed",
      "habitat_condition": "low on hay",
      "welfare": "unsatisfied"
    },
    {
      "id": "3",
      "animal_id": "3",
      "food": "fresh fruits",
      "habitat_condition": "good",
      "welfare": "happy"
    },
    {
      "id": "4",
      "animal_id": "4",
      "food": "medicine",
      "habitat_condition": "excellent",
      "welfare": "anxious"
    },
    {
      "id": "5",
      "animal_id": "5",
      "food": "fish",
      "habitat_condition": "good",
      "welfare": "restless"
    },
    {
      "id": "6",
      "animal_id": "6",
      "food": "fish",
      "habitat_condition": "good",
      "welfare": "restless"
    },
    {
      "id": "7",
      "animal_id": "7",
      "food": "fish",
      "habitat_condition": "good",
      "welfare": "restless"
    },
    {
      "id": "8",
      "animal_id": "8",
      "food": "fish",
      "habitat_condition": "good",
      "welfare": "restless"
    },
    {
      "id": "9",
      "animal_id": "9",
      "food": "fresh fruit",
      "habitat_condition": "good",
      "welfare": "content"
    },
    {
      "id": "10",
      "animal_id": "10",
      "food": "fresh fruit",
      "habitat_condition": "good",
      "welfare": "tired"
    },
    {
      "id": "11",
      "animal_id": "11",
      "food": "fresh fruit",
      "habitat_condition": "good",
      "welfare": "hyperactive"
    }
  ]
}
```

     


