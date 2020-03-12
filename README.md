# Regex Tutorial

Useful rules and concepts that make it easy to understand Regex. 
**Regex** is a special string that enables to define any search pattern. It is helpful when we want to be able to search for entries that vary but have an underlying pattern. It is implemented in Java, C and Python. They are nearly identical but with minor differences and this tutorial will focus on **Python** "flavour". 

**Important to know that search in regex is not overlapping e.g. if we are searching for 'aa' in the following text:**
- aaaa
The result will have only 2 matches with the positions [0:2, 2:end].
But it does not consider 1:3 as a match. 


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

## Switch to another file

pattern = re.compile(r '\d\d\d' )
matches = pattern.finditer(text)

it will find any occurence of 3 numbers in a row. 

If we want it to find something like 367-980-909 or 908.444.343 or 676 890 565
pattern = re.compile(r '\d\d\d.\d\d\d.\d\d\d')
dot means any character 

if we want the separator for the phone number to be only - or . 
we need special character **[]** so pattern is 
pattern = re.compile(r '\d\d\d [-.] \d\d\d [-.] \d\d\d') *obv withous spaces*

**We dont need escaping in character set. Even if character set has two characters inside it will only match one of them** so not 367--897.898!!

we want to match only patterns that start with 800 or 900
pattern = re.compile(r '[89]00 [-.] \d\d\d [-.] \d\d\d')

we want to match only digit from one to 5 pattern = re.compile(r '[1-5]')
we want to match only lowercase letters pattern = re.compile(r '[a-z]')
lowercase and uppercase = re.compile(r '[a-zA-Z]')

^ inside a character set negates everything inside of a character set, we want to match only characters that are not lowercase letters pattern = re.compile(r '[^a-z]')

cat rat mat bat ( we want to match cat and rat but not bat ) 
pattern  = re.compile(r '[^b]at')

INSTEAD pattern = re.compile(r '\d\d\d [-.] \d\d\d [-.] \d\d\d') 
we can write pattern = re.compile(r '\d{3} [-.] \d{3}[-.] \d{3}')

( ) groups allow us to match several different patterns and we need to use | inside of a group 


Mr. Schafer Mr Smith Ms Davis Mrs. Robinson Mr. T
1) to match Mr and Mr. 
pattern = re.compile(r 'Mr\.?') 
dot escaped so it means exactly a dot and also optional bc after it comes ?
2) with names
pattern = re.compile(r 'Mr\.?\s[A-Z][a-z]*')  
\s is one space, and [A-Z] one uppercase letter and then [a-z]*\* means 0 or more lowercase letters
3) if we want to include Ms and Mrs too
pattern = re.compile(r 'M(r|s|rs)\.?\s[A-Z][a-z]*')   or 
pattern = re.compile(r '(Mr|Ms|Mrs)\.?\s[A-Z][a-z]*')

lutur-kutur@gmail.com
lutur.kutur@gmail.edu
lutu123.kutur@gmail.net

(r'[a-zA-Z0-9.-]+@[a-zA-Z]+(com|edu|net)

urls = """
 https://www.google.com
 http://coremys.com
 https://youtube.com
 https://www.nasa.gov
 """

(r'https?://(www\.)?\w+\.\w+)

similarily if we group all of the domain names (google, coremys, youtube, nasa) and we group (.com and .gov)
r'https?://(www\.)?(\w+)(\.\w+)'

when we print out matches we can print them out by saying match.group(0) which prints the whole match, and group one is an optional www. group 2 is domain name and group 3 is .com or .gov

and now if we wanted to substitute all of the matches with just domain name and extension we 
pattern = r'https?://(www\.)?(\w+)(\.\w+)'
subbed_urls = pattern.sub(r'\2\3' , urls)

subber_urls = '''
google.com
coremys.com
youtube.com
nasa.gov '''


## Methods
patter.findinder
pattern.findall - just returns matches
pattern.match - checks if the pattern is on the beginning of the string, if no then it doesnt return anything
pattern.search - returns just first match

## Flags

pattern = (r'start' , re.IGNORECASE) it means ignore case 
re. I = re.IGNORECASE

