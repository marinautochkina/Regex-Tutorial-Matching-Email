# Regex Tutorial: matching Email

Regular expressions, often referred to as regex, are a powerful tool used in programming and text processing to search, match, and manipulate strings based on specific patterns. They provide a concise and flexible syntax for defining complex search criteria, making them invaluable for tasks such as data validation, information extraction, and text transformation.

## Summary

In this tuttorial, we will explore a regular expression designed for matching and validating email addresses. The regex pattern captures the essential components of a valid email format, including the local part, the "@" symbol, and the domain. By using this regex, you can ensure that user inputs conform to standard email conventions, which is crucial for any application that relies on email communication.

``const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;``

We’ll explain how the different components of this regex come together to ensure that email addresses are correctly formatted.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Regex anchors are special characters that allow you to specify the position of a pattern within a string rather than matching specific characters. They help define the boundaries of where a match can occur, enabling more precise searches. The two most common anchors are:

- Caret (^):

This anchor asserts that the match must occur at the beginning of a string.
Example: In the regex ^Hello, it will match the string "Hello, world!" but not "Say Hello".

- Dollar Sign ($):

This anchor asserts that the match must occur at the end of a string.
Example: In the regex world!$, it will match "Hello, world!" but not "world! is great".


### Quantifiers

Quantifiers play a crucial role in email regex patterns by defining how many times certain characters or groups can appear. Here's a breakdown of how quantifiers can be applied specifically in the context of matching email addresses:

1. Asterisk (*): Matches zero or more occurrences of the preceding character or group. Example: In .*, it can match any characters in the local part of an email, including none.

2. Plus (+): Matches one or more occurrences of the preceding character or group.
Example: In the pattern [a-zA-Z0-9._%+-]+, the + ensures that the local part of the email must contain at least one valid character.

3. Question Mark (?): Matches zero or one occurrence of the preceding character or group, making it optional.
Example: In @?, it can be used to indicate that the "@" symbol is required but could follow certain optional conditions.

4. Braces ({n}): Matches exactly n occurrences of the preceding character or group. Example: In \.{2}, this would require exactly two dots, which is not common in emails but illustrates the usage.

5. Range Braces ({n,m}): Matches between n and m occurrences of the preceding character or group. Example: In the pattern [a-zA-Z]{2,}, this would require the top-level domain to have at least two letters (e.g., ".com", ".org").

### Grouping Constructs

 Grouping constructs are used to define specific parts of a pattern and apply quantifiers or other operations to those groups as a whole. In the context of email regex, grouping can help manage different components of an email address, such as the local part, the domain, and the top-level domain (TLD). Here are some common grouping constructs used in email regex patterns:

1. Parentheses (): Parentheses are used to create groups in regex. They allow you to apply quantifiers to an entire group or to capture parts of the match for further processing. Example: In the regex ([a-zA-Z0-9._%+-]+)@([a-zA-Z0-9.-]+)\.([a-zA-Z]{2,}), the parentheses group the local part, the domain, and the TLD separately.

2. Capturing Groups: Groups defined by parentheses capture the matched text, which can be referenced later in programming languages or by back-referencing in regex patterns. Example: The pattern ([a-zA-Z0-9._%+-]+)@([a-zA-Z0-9.-]+)\.([a-zA-Z]{2,}) captures the local part, domain, and TLD as separate groups.

3. Non-Capturing Groups (?:...): These groups are defined using (?:...) and allow you to group patterns without capturing the matched text. This can be useful for applying quantifiers without storing the match.
Example: (?:[a-zA-Z0-9._%+-]+) can be used to group the local part without capturing it

### Bracket Expressions

Bracket expressions allow to define a set of characters to match. In the context of email regex, bracket expressions help specify which characters are valid in different parts of an email address, such as the local part and the domain. Here’s a detailed overview:

Common Bracket Expressions in Email Regex

1. Basic Character Class: A set of characters defined within square brackets [...] matches any single character from the set. Example: [a-z] matches any lowercase letter from 'a' to 'z'.
2. Combining Ranges:You can combine ranges and individual characters within the same bracket expression. Example: [a-zA-Z0-9] matches any alphanumeric character (both lowercase and uppercase letters and digits).

3. Including Special Characters: You can include special characters in the bracket expression as well. Example: For the local part of an email, you might use [a-zA-Z0-9._%+-], which includes letters, digits, and common special characters allowed in email addresses.

4. Negated Character Class: A negated character class, defined as [^...], matches any character not in the specified set. Example: [^@] matches any character except for the '@' symbol.

### Character Classes

Character classes allow us to match a range of characters. In the email regex:

[a-zA-Z] matches any uppercase or lowercase letter.`

[0-9] matches any digit.

These classes are useful for ensuring that domain names and TLDs are composed of letters and/or numbers.

### The OR Operator

You can use the OR operator to match different valid characters or structures in an email address.
Example: To allow either "gmail.com" or "yahoo.com" as valid domains, you could use:

``^[a-zA-Z0-9._%+-]+@(gmail\.com|yahoo\.com)$``

### Flags

Flags (also known as modifiers) are special options in regular expressions that change how the pattern is processed. They can be used to modify the behavior of the regex engine, allowing for more flexible and powerful matching. 
There are several common flags used to match email: 

1. Global Flag (g): used if you want to match multiple email addresses in a single input string.
2. Case-Insensitive Flag (i): Essential for accurately validating emails, as it allows for variations in letter casing.3. 
Multiline Flag (m): Useful when processing emails line by line, such as in a file.

### Character Escapes

Character escapes are used to treat special characters as literal characters. This is particularly important in email regex, where certain characters have specific meanings in regex syntax. Here’s a detailed overview of how character escapes are used in email regex patterns:

Commonly Escaped Characters

1. Dot (.): In regex, a dot matches any character except for a newline. To match a literal dot (as found in email addresses), you need to escape it.
Usage: \. Example: In the pattern @example\.com, the backslash (\) ensures that the dot is treated as a literal character.

2. At Symbol (@): The @ symbol does not need to be escaped in regex. However, it is often included in patterns without escape. Example: ^[a-zA-Z0-9._%+-]+@ is valid without escape.

3. Hyphen (-): Inside square brackets, a hyphen is used to specify a range (e.g., [a-z]). To match a literal hyphen, it should be placed at the start or end of the character class or escaped. Usage: [-] or just place it at the start or end, like [a-zA-Z0-9._%+-].

4. Plus (+) and Asterisk (*): Both of these characters have special meanings in regex (matching one or more, and zero or more, respectively). When used literally, they should be escaped. Usage: \+ or \* when they need to be matched as characters.

5. Question Mark (?): This character also has special meaning (matching zero or one occurrence). To use it literally, it must be escaped. Usage: \? if it appears in a regex pattern.

## Author

This Turorial was written by [GitHub @marinautochkina](https://github.com/marinautochkina)
