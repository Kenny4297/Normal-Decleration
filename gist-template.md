# Regular Expressions Tutorial

RegEx, or 'regular expressions', is a specific language for describing patterns in strings. They are often used for text processing, data validation, and search & replace operations in many programming languages. A RegEx consists of a sequence of characters that define a search pattern. They are powerful tools that allow you to preform complex text manipulation tasks with relatively simple code. 

I would like to analyze a specific RegEx that is commonly used to test password strengths of moderate security. The RegEx under observation checks to see if the user is using at least 1 lowercase letter, 1 uppercase letter, 1 number, 1 special character, and be at least 8 characters long. 
The RegEx under observation: <br />
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />
* The ```/\``` only signify the beginning and ending of the RegEx. They do nothing else.

## Vocabulary
"string" = the physical representation of the regular expression itself <br />
Example: 'asdofjoi208j' is the string for the regular expression <br /> <br />
"match" = acceptable parameters <br /> 
Example: "This string matches the regular expression" means "This string is acceptable for the regular expression" <br />

## Overview
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />
I know that must have seemed confusing, so let's take a final look at what's going on here:
* The string must contain a digit (```[0-9]```);
* The string must contain an alphanumeric character (```[A-Za-z0-9]```);
* The string must contain an uppercase letter (```[A-Z]```);
* The string must contain a lowercase letter (```[a-z]```);
* The string must contain at least 8 characters ( ```.{8,}```);

The regEx uses a few tricks to enforce these measures. 
* The ```(?=(.*[0-9]))``` **look-ahead**, combined with the ```.*``` **quantifier**, makes sure that the string must contain at least one digit. The ```()``` group together the certain conditions of each section of the string.
* The supper-massive **look-ahead** ```((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))``` groups these three **look-aheads** together inside a set of parentheses, enforcing that all three conditions must be met in order for the string to be acceptable. 
* Finally the ```^.{8,}$``` states that the string must be at least 8 characters long. <br />

Here is an example of an acceptable string for the current regular expression: <br />

9aHj8bKm

I have a feeling this doesn't make sense, and that's ok! Let's dive into each concept.

## Table of Contents

- [Character Classes and Ranges](#character-classes-and-ranges)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Quantifiers](#quantifiers)
- [Bracket Expressions](#bracket-expressions)
- [Grouping and Capturing](#grouping-and-capturing)
- [Anchors](#anchors)
- [OR Operator](#or-operator)
- [Flags](#flags)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Summary](#summary)
- [Author](#author)

## Regex Components
Components, also known as *atoms*, are the building blocks of regular expressions. We will be taking a look at these while breaking down our RegEx in question within the following sections.

## Character Classes and Ranges
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />

Let's start with the easy part. **Character classes** represent a list of characters enclosed by the square brackets. We see a few of them in the RegEx: <br />
```[0-9]```, ```[A-Za-z0-9]```, ```[A-Z]```, ``` [a-z]``` <br />
We also notice that there is a '-' inside our brackets. When this is the case, this means that there is a **range**. Take a look at the first **character class**. In this specific expression, it means that this RegEx must contain a digit, or in other words, a digit from 0 to 9.
* The second **character class** tells us that the string must contain an alphanumeric character (indicated by ```[A-Za-z0-9]```).
* The third tells us that an uppercase letter must be included (indicated by ```[A-Z]```).
* The last **character class** tells us that the string must contain a lowercase letter (indicated by ```[a-z]```).
* There is more to this than what I previously stated, but that will be discussed later. 

## Look-ahead and Look-behind
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />

Now that we have deciphered all the **character classes**, let's take a look at the stuff before the classes, specifically the ```(?=...)```. This is called a **look-ahead**. In this specific code, the **look-aheads** makes sure that the string ***must contain at least one*** character class that is inside its brackets. Let's break down our sections with the **look-aheads**. Our code should look somewhat like this:
* ```(?=(.*[0-9])``` (at least one digit from 0-9) 
* ```(?=.*[A-Za-z0-9])``` (at least one alphanumeric characters)
* ```(?=.*[A-Z])``` (at least one uppercase letter) 
* ```(?=.*[a-z])``` (at least one lowercase letter) <br />
*Note: Keen observers see that there is a larger, more menacing **look-ahead**.* <br /> 
```((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))```.  <br /> 

*By grouping these three **look-aheads** together inside a set of parentheses, the overall regular expression enforces that all three conditions must be met in order for the string to match*

*Another note: This example does not have any **look-behinds***

But what about the (```.*```)? Great question!!

## Quantifiers
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />

What are the (```*```) and (```.```) we see? Those are called **Quantifiers**. These quantifiers enforce the criteria of the string.

When these asterisks are alone, they specify the number of times the following pattern can occur. <br />

We see a few cases of the (```.```). This acts as an "all" character. <br />

When as asterisk combined with a (```.```) to make a (```.*```), they create a new **quantifier** that matches all the characters in the **character class**, plus zero or more characters of any kind, meaning there can be as many characters (or none) in the respective **character class** as the user wants. <br /> 

***But wait!*** Doesn't the prase "*there can be as many characters **(or none)** in the respective **character class** as the user wants*" mean I can just omit that character class? <br />

Doesn't that mean that I can choose to have zero characters of any **character class**? <br /> 

Wouldn't that mean that a blank string would be valid since I'm choosing to have zero **characters classes**? <br />

You would be correct, but you overlooked a tiny detail: The **look-ahead** makes sure that there is *at least one character* of the **character class** present! It "*adjusts*" the definition of the (```*```) from "*zero or more characters of any kind*" to "*at least one*" character of any kind.

We also see another **quantifier**, the ```{8,}``` at the end. This indicates how many characters the string must have. Since the number is '8', the following regex would not not be acceptable: <br />  au186Da -> this matches the criteria presented in the **character classes** (at least 1 digit, at least 1 alphanumeric character, etc), but it is not 8 characters long!

Let's see these **quantifiers** in combination with a few more components below.

## Bracket Expressions
Even though we see brackets, no **bracket expressions** exist in this RegEx! Remember that those brackets in this RegEx are indicating a **Character Class**!

## Grouping and Capturing
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />
**Grouping** (using ```()```) allows you to group multiple Regex's together so that you can apply operators or **quantifiers** to the entire group, not just individual characters. In our sample code, grouping is used to group the **look-aheads**, as you can tell by the use of parentheses(```()```). Review the notes on the **"Look-ahead and Look-behind"** section for a better understanding on grouping. Keep in mind that **capturing** is not used in this RegEx.

## Anchors
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />

**Anchors** are sequencies that match an empty substring: <br />
```^``` -> indicates the beginning of the string. In this example, anything to the left of the (```^```) is the string itself. This can be used to separate the string itself from the criteria of the string (```{8,}```). <br />
```$``` -> indicates the end the string, similar to punctuation at the end of a sentence. <br />
```/b``` -> matches a **word boundary**, something that is not used in our code sample. <br />
These are always used in combination with some other **quantifier** or operator.

## OR Operator
Unfortunately there are no **OR operators** in this RegEx. The **'OR operator'** is typically represented by a pipe symbol ```|``` and is used to match either one of several alternatives. Oh well.

## Flags
Unfortunately, there are also no **flags** in our expression. **Flags** are special characters that modify the behavior of the RegEx. Some common **flags** include ```i``` (for case-insensitivity), ```m``` (for multi-line matching), and ```s``` (for single-line matching). **Flags** are typically placed after the closing forward slash ```/``` of the regular expression. How cool!

## Greedy and Lazy Match
Once again, there are no **Greedy Or Lazy Matches** in this code. Thank goodness for that. Who likes lazy people? 

## Boundaries
There are no **boundaries** in this RegEx. 

## Back-references
As much as I tried to confuse you, there are no **back-references** used in this RegEx either.

## Summary
```/(?=(.*[0-9]))((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.{8,}$/``` <br />
Let's recap on what is going on here:
* The string must contain at least one digit (```(?=(.*[0-9]))```);
* The string must contain at least one alphanumeric character (```(?=.*[A-Za-z0-9])```);
* The string must contain at least one uppercase letter (```(?=.*[A-Z])```);
* The string must contain a lowercase letter (```(?=.*[a-z])```);
* The supper-massive **look-ahead** ```((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))``` groups these three **look-aheads** together inside a set of parentheses, enforcing that all three conditions must be met in order for the string to be acceptable;
* (```^```)---> Anything to the left of this is the string itself. Anything to the right are the criteria for the string;
* The string must contain at least 8 characters ( ```.{8,}```);

Let's take a look at a valid string, and an invalid string: <br />
**Valid:** <br />
```4aRibHk9``` -> This is a valid string. It contains at least all of the **character class** requirements (see the bullet points above), and is at least 8 characters long. 
* Keep in mind that the order of the **character class** doesn't matter! In other words, as long as you have all the **character class** requirements (again, see the bullets above), you can have them in any order for the string to be acceptable.
* Also understand that the ```^.{8,}$``` has nothing to do with the physical part of the string! Similar to the ```[]```, they are parts of the regular expression that act as criteria for the string in question.

**Invalid:** <br />
```AaBbCcDd```
* Ok, It's 8 characters long, but does not contain a digit.

```4aRibHk```
* Meets all the **character class** requirements, but is not 8 characters long.

## Author
About the Author: Ked is a self taught M(S)ERN stack web developer with over a year of experience. He learned about RegEx when studying Python in late 2021, and has already used it a few previous Bootcamp assignments. 

Github repo: https://github.com/Kenny4297