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
	. \d \D \w	\W \s \S \b \B ^ $
- *normal characters* - most of the characters alone stand exactly for that character 

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
