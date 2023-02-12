# Normal Declarations (a RegEx tutorial)

RegEx, or 'regular expressions', are a specific language for describing patterns in strings. They are often used for text processing, data validation, and search and replace operations in many programming languages. I regex consists of a sequence of characters that define a search pattern. They are powerful tools that allow you to preform complex text manipulation tasks with relatively simple code. 

## Summary
I would like to analysis a specific RegEx that is commonly used to test password strengths of moderate security. This RegEx checks to see if the user is using at least 1 lowercase letter, 1 uppercase letter, 1 number, 1 special character, and be at least 8 characters long. Keep in mind that any of these qualifications can exist anywhere in the password; meaning there is no order that these qualifications need to be met at. 
The RegEx under observation:
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/```

At first glance this seems like complete madness, and it is. But upon further inspection you will understand what each section does and why it is necessary to 

-----(Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.)

## Table of Contents

- [Character Classes](#character-classes)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Bracket Expressions](#bracket-expressions)
- [Grouping and Capturing](#grouping-and-capturing)
- [Quantifiers](#quantifiers)
- [Anchors](#anchors)
- [OR Operator](#or-operator)
- [Flags](#flags)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Summary](#summary)
- [Author](#author)

## Regex Components
Components, also known as *atoms*, are the building blocks of regular expressions. We will be taking a look at these while breaking down out RegEx in question, previously stated.
## Character Classes and Ranges
Let's start with the easy part. character classes represent a character set in regards to a list of characters enclosed by the square brackets. We see a few of them in the RegEx:
```[0-9]```, ```[A-Za-z0-9]```, ```[A-Z]```, ``` [a-z]```
We also notice that there is a '-' inside our brackets. When this is the case, this means that there is a **range**. Take a look at the first character class. In this specific expression, it means that this RegEx must contain at least one digit.
* The second character class tells us that the string must contain at least one alphanumeric character (indicated by [A-Za-z0-9]).
* The third tells us that at least one uppercase letter must be included (indicated by [A-Z]).
* The last character class tells us that the string must contain at least one lowercase letter (indicated by [a-z]).
* There is more to this that we will get into in the future, but for now this will do. 

## Look-ahead and Look-behind
Now that we have deciphered all the character classes, let's take a look at the stuff before the classes, specifically the ```(?=...)```. This is called a Look-ahead. In this specific code, this is used to make sure that the pattern inside the lookahead matches at the current position in the input string, but without using any characters. Let's break down our sections with the look-aheads. Our code should look somewhat like this:
```(?=(.*[0-9])```, ```(?=.*[A-Za-z0-9])```,```(?=.*[A-Z])```, ```(?=.*[a-z])```
*Note: Keen observers see that there is a larger, more menacing look-ahead. ```((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))```.  By grouping these three look-aheads together inside a set of parentheses, the overall regular expression enforces that all three conditions must be met in order for the string to match*
*Another note: This example does not have any look-behinds*

Alright, so we now know that each section listed above begins with a 'look-head', followed by the criteria of the code. But what about the '.' and '*'?

## Bracket Expressions
Even though we see brackets, no bracket expressions exist in this RegEx! Sorry!!

## Grouping and Capturing
Grouping allows you to group multiple Regex's together so that you can apply operators or quantifiers to the entire group, not just individual characters or sub-expressions. In our sample code, grouping is used to group the look-aheads, and you can tell by the use of parentheses. Read the notes on the previous section for a better understanding on grouping. Keep in mind that capturing is not used in this RegEx.

## Quantifiers
To answer your fantastic question, the ```*``` are called Quantifiers. When these asterisks are alone, they specify the number of times the preceding pattern can occur. When combined with a ```.``` to make a ```.*```, they create a new quantifier that matches zero or more characters of any kind, meaning there can be as many characters in the following character class as the user wants. Now the snippets in the 'Look-ahead' stated above start to make sense!


## Anchors
Anchors are sequencies that match an empty substring:
```^``` -> matches the beginning of the string (believe it or not, we do not have any of these anchors in our code! More on this later)
```$``` -> matches the end of the string
```/b``` -> matches a word boundary, something that is not used in our code sample
These are always used in combination with some other quantifiers or operators.

## OR Operator
Unfortunately there are no OR operators in this RegEx. The 'OR operator' is typically represented by a pipe symbol ```|``` and is used to match either one of several alternatives. Oh well.

## Flags
Unfortunately, there are also no flags in our expression. Flags are special characters that modify the behavior of the pattern in question. Some common flags include ```i``` (for case-insensitivity), ```m``` (for multi-line matching), and ```s``` (for single-line matching). Flags are typically placed after the closing forward slash ```/``` of the regular expression. How cool!

## Greedy and Lazy Match
Once again, there are not Greedy Or Lazy Matches in this code. Thank goodness for that. Who likes lazy people? 

## Boundaries
I hoped that I tricked you at the beginning of the lesson. When I said that we don't have any ```^``` anchors, I am still not lying to you. What we see here is in fact a ```^```, but the role it plays is not one of an anchor, but of a boundary. The ```^``` boundary is used to match the start of the string. It makes sure the code pattern matches only if it is at the very beginning of the string, and not just anywhere in the entire string. The ```$``` is also a boundary, signifying where the string ends. Here, it makes sure that the string being matched is at least 8 characters long and ends the string with any character. The ```.{8,}``` part of the RegEx specifies that there must be at least 8 characters  in the string. This ties up the pattern by making sure the string ends with those 8 or more characters.

## Back-references
As much as I tried to confuse you, there are no back-references used in this RegEx.

## Summary
I know that must have seemed confusing, so let's take a final look at what's going on here:
* The string must contain at least one digit (```[0-9]```);
* The string must contain at least one alphanumeric character (```[A-Za-z0-9]```);
* The string must contain at least one uppercase letter (```[A-Z]```);
* The string must contain at least one lowercase letter (```[a-z]```);
* The string must contain at least 8 characters ( ```.{8,}```);

The regEx uses a few tricks to enforce these measures. 
* The ```(?=(.*[0-9]))``` look-ahead makes sure that the string must contain at least one digit. The ```.*``` before the look-ahead allows an infinite number of characters to be used from the look-ahead.
* The supper-massive look-ahead ```((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))``` groups these three look-aheads together inside a set of parentheses, enforcing that all three conditions must be met in order for the string to match. 
* Finally the ```^,{8,}$``` states that the string must be at least 8 characters long and must be matched from the start of the string to the end.


## Author
About the Author: Ked is a self taught M(S)ERN stack web developer with over a year of experience. He learned about RegEx when studying Python in late 2021, and has used a few in the previous Bootcamp assignments. 

Github repo: https://github.com/Kenny4297

(A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
