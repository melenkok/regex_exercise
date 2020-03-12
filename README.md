# Regex Tutorial

Useful rules and concepts that make it easy to understand Regex. 
**Regex** is a special string that enables to define any search pattern. It is helpful when we want to be able to search for entries that vary but have an underlying pattern. It is implemented in Java, C and Python. They are nearly identical but with minor differences and this tutorial will focus on **Python** "flavour". 

**Important to know that search in regex is not overlapping e.g. if we are searching for 'aa' in the following text:**
- aaaa
The result will have only 2 matches with the positions [0:2, 2:end].
But it does not consider 1:3 as a match. 

## Funtions to search


# Different charachters

In Regex we have: 
- *special characters*  - need to be escaped
.	^	$	*	+	?	{	}	[	]	\	|	(	)
- *meta characters* - one sign considers a group of characters (or a principle) e.g. a dot **"."** stands for any character
- *quantifiers* - they multiply the number of times specific condition will be met
\* + ?  {number} {min number, max number}
	. \d \D \w	\W \s \S \b \B ^ $
- *normal characters* - most of the characters alone stand exactly for that character 

## Quantifiers

- **\*** 0 or more
- **+**  1 or more
- **?** 0 or 1
- **{3}** exact number (in this example 3 times)
- **{3,5}** minimum 3 times but maximum 5 times

## Meta characters 

- **\d** any digit (0-9)
- **\D** not a digit
- **\w** word character (a - z, A - Z, 0 - 9, _ )
- **\W** not a word character
- **\s** whitespace (space, tab, newline)
- **\S** not a whitespace (space, tab, newline)
- **\b** word boundary (meaning just the start of the word)
- **\B** not a word boundary
- **^** beginning of a string
- **$** end of a string

## Brackets

- **[ ]** called character set. it means that the pattern currently being matched can be any of the characters in the character set
**characters to be picked from the character set don't need to be escaped **
>Example 1.  We want to match following patters:
> 367-980-909 and 908.444.343 

pattern = re.compile(r '\d\d\d[-.]\d\d\d[-.]\d\d\d')

>Example 2.  From the text "cat rat mat bat lat hat" we want to match all the words except for "mat" bat"

**^ inside of a character set negates the pattern in character set**
pattern  = re.compile(r '[^bm]at')



- **{ }** quantifier that can indicate how many same patterns
> 367-980-909 and 908.444.343

pattern = re.compile(r '\d{3}[-.]\d{3}[-.]\d{3}')

- **( )** that comes with **|** . It is called a GROUP set. It is similar to character set just that it allows us to say OR between GROUPS of patters. 

**Characters inside of a group patter need to be escaped if they are special characters**

>Example 3.  We want to match following patters:
>"Ms Sunshine" , "Mr Naughty" , "Mr. Clumsy" and "Mrs Kind"

pattern = re.compile(r '(Mr|Ms|Mrs)\.?\s[A-Z][a-z]*')

>Example 4.  We want to match following patters:
>"Ms Sunshine" , "Mr Naughty" , "Mr. Clumsy" and "Mrs Kind"

## Group example

>From this text we want to be able to match all of the urls
>urls = '''
 https://www.google.com
 http://coremys.com
 https://youtube.com
 https://www.nasa.gov
 '''

pattern = re.compile(r'https?://(www\.)?(\w+)(\.\w+)')
*explanation:*
*https?*  **http and s that is optional**
*://*  **semicolon and two backslashes
*(www.)?* **1st group that is optional**
*(\w+)* **2nd group which contains lowercase word characters**
*(\.\w+)* **3rd group which contains a .com or any other patter which has a dot and letters**

>If we now want to replace each url in urls multistring text we can use the group property. In the next example we will replace each url with 2nd and 3rd group.

subbed_urls = pattern.sub(r'\2\3' , urls)

>subbed_urls = '''
 google.com
 coremys.com
youtube.com
nasa.gov
 '''

## Flags

If we use flags we can make our search easier. Suppose we want to find either
>START or start or StaRt or any combination case-wise

pattern  = re.compile(r'(S|s)(T|t)(A|a)(R|r)(T|t))
 OR
 pattern = (r'start' , re.IGNORECASE)
