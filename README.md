# Password

I understand that no password is truly uncrackable but given the scope of resources and time needed to crack these passwords it would be rather difficult.
This code is a continuation and expansion of the code of a password generator that Johan Godino made to try and make a random generator. While that is certainly a helpful program, I have tried to expand the project even further by making the project more user friendly and making it so that any person could memorise the password given. You can find a link to the original video of a random password generator here.
The core functionality of this program is that it builds passwords from things you like. It will ask the user for 3 inputs. First, an input of a place they like/ have visited then 2 inputs of words that they like.
To start off you would need to import the relevant libraries.
For this project, there are two main libraries that will be used
Random which is inbuilt to python and nltk which is one of the best machine learning libraries when working with natural language. #
You need to install nltk on your machine if you do not have it already built-in. If so run
Pip install nltk
This should install the library. As nltk does have not all the data you will need will be prebuilt in so you might need to run
Nltk.download(‘omw-1.4’)
First, we should define some of the local variables that we are going to use:
The most important one is going to be the local variable known as password this is where we are going to store the string of characters that make up the password.
Secondly, we need to set a variable special character that contains all the special characters that we will use to split the different words that will make up the password. The reason to use special characters is from a UX perspective in terms of being able to make the words more memorable as if we split the words based on letters it will look like muddled words that could be confusing for the user. In the worst-case scenario, if two of the words combine it could create a word that already exists and could confuse the user even further.
Ok with the two local variables set we want to move onto some of the functionality first I used a lambda expression to pick a random character from the special characters using random.choice. Then moved into adding a copy of the same character and adding them both to the password. I defined them both as functions in order to be able to reuse them later.
Next comes the simplest aspect of the program asking the user for input in terms of their favourite place to go on holiday or that they have been and attaching that to the password variable. As the special character selector and doubler have been defined than add that to the password as well after the location.
Then moved on to what is arguably the most difficult aspect of the program, which uses machine learning. We will be defining a new nested function; within this function, we want to create a list. You then want to call a Synset for loop on their favourite word that they input. Synset is part of the NLP branch of machine learning, but it finds synonyms for the words input sometimes it will only have an exact match. Other times there could be many synonyms for the word. I then ran a nested for loop to lemmatize the synonym words.
What is lemma
A lemma is the shortening of a word to return to its base form. A great example of this would be the word running instead of it being running what would be input into the list would be run as the run is the base form of running.
Once you have done that it is straight forward all you must do is attach the chosen synonym to the password. Then repeat the process of attaching another synonym of a user inputted word and for the final section attaching a 2-digit number towards the end.
The result:
I think it is good to measure how effective these passwords are so I have run them through a password strength checker which can be found at https://bitwarden.com/password-strength/. All of them came back as centuries which I think is good enough to say that these passwords are good enough for time being.
I ran this test three times
The first time my inputs were:
Stockholm
Snow
Fire
The resulting password was:
“”Stockholm^^lead_by_the_nose%%terminate9
My second time I used the inputs of:
London
Football
Poker
The resulting password was:
^^london[[football_game@@poker56
My third time:
Berlin
Food
Party
The third result was:
“”Berlin^^food>>company79
As you can see these passwords are generally quite memorable but are also easier to remember than randomly generated passwords. There are still some upgrades that would improve this such as removing exact matches. But I will leave that up to you in the case that you feel like doing a challenge.
This is quite a simple use of machine learning in terms of NLP you are not really analysing the use of the words but it gives a great understanding of how you can use a library to allow for interesting features.
If you are wanting a challenge and or to improve the project here are some ways to do so.
3 ways to improve the project
1. Switch the positions of the words and the location so that the location is not always first but will be attached at a random position.
2. Switch it so it can become more relevant to the user by allowing the user to add a number that they find relevant to their own life e.g birth year, graduation year rather than some randomly generated numbers
3. Make it so that exact matches of the word inputted aren’t possible to be inserted into the password.
You can find a link to the GitHub here.
The full code for this is:
from random import random
import nltk
from nltk.corpus import wordnet
import random
#you will need to download this data set if you do not already have it loaded as it does not come preinstalled with NLTK
#nltk.download('omw-1.4')
def password_generator():
password = ''
special_Characters  = '!"£$%^&*()[]:;@#~?<>'
divider = lambda x: random.choice(x)
doubler = lambda x: x + x
password = doubler(divider(special_Characters))
city = input('What is a city you like that you have visited?')
password = password + city + doubler(divider(special_Characters))
word1 = input('What is a word that you like (do not type a name) ')
def synonym(x):
synonym_list =[]
for syn in wordnet.synsets(x):
for lemm in syn.lemmas():
synonym_list.append(lemm.name())
return random.choice(synonym_list)
password = password + synonym(word1) + doubler(divider(special_Characters))
word2 = input('What is a second word that you like (do not type a name) ')
password = password + synonym(word2) + str(random.randint(0,99))
return print(password)
password_generator()
Mlearning.ai Submission Suggestions
How to become a writer on Mlearning.ai
medium.com
