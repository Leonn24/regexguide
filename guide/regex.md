# Understanding the Components of Regex

Welcome to this comprehensive tutorial on matching email regular expressions (regex) using JavaScript in the field of Computer Science.

## Summary

Throughout this tutorial, the featured regular expression (regex) as seen below, will be referenced for analysis in regards to each regex component. The regex components discussed in this document include: anchors, quantifiers, grouping constructs, bracket expressions, character classes, the OR operator, flags, and character escapes.

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
Anchors, which are special characters in regular expressions, play an essential role in defining the position of the pattern within the input string. In the context of email validation, like in the regex featured in this example ```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/``` it is IMPORTANT to ensure that the entire input string matches the specified pattern.

#### Anchors come in 2 Types:

First: Start Anchors ```^``` asserts that the pattern must match the ```START``` of the string.
Second: End Anchors ```$``` asserst that the pattern must match the ```END``` of the string.

Anchors define the limits of the text that the regular expression should match. 

```Example One``` the regex ```^World$``` matches only the string "World" and nothing else. It won't match "Hello World" becuase the pattern is not at the start or end of the string, repspectively.

```Example Two``` the regex ```^hello``` matches any string where "hello" is at the start of the string. It WILL match "hello" in "hello world", but it will not match "hello" in "world hello" because the string doesn't start with "hello".

In the context of email validation, anchors play an imporant role because it ensures that the entire email address follows the specified pattern. This is important for accurate validation, because it prevents partial matches or unwanted results. By setting boundaries at the start and end of the string, anchors guarantee that the pattern matches only the intended text. In conclusion, anchors play an imporant role in defining the position of the pattern within the input string and ensure accurate and reliable validation.

### Quantifiers
In regex, quantifiers are used to define how many times a pattern should match. Quantifierss are placed at the end of an element/character or group.

The `*` quantifer means ZERO or MORE, and used after the pattern `[a-z0-9_\.-]` would end up looking like this `([a-z0-9_\.-]*)`. This would indicate that the pattern would match an empty string or have more occurances.

The `?` quantifer means ZERO or ONE, and used after the pattern `[a-z0-9_\.-]` would end up looking like this `([a-z0-9_\.-]?)`. This would indicate that the pattern would match an empty string or have only ONE occurance.

If we put it all together, the regex would something like this `/^([a-z0-9_\.-])?@([\da-z0-9_\.-])\.([a-z\.]{2,6})`. This would match a valid email address that starts zero or more lowercase letters, numbers, underscores, dots, or hyphens, followed by the `@` symbol, followed by one or more numbers, lowercase letters, dots, or hyphens, followed by a period and two to six letter top-level domain.

### Grouping Constructs
Grouping constructs in regex are used to group together one or more characters or sub expressions, and treats them as a single unit within the expression. They are enclosed among the parentheses `()` and serve the following purposes:

`Applying quantifiers to a group of characters`

`Capturing the designated part of the match for later use`

`Creating backreferences for previously matched group`

`Applying alternation to a group of characters`

The regex featured above `/^([a-z0-9_\.-])?@([\da-z0-9_\.-])\.([a-z\.]{2,6})` includes 3 `Grouping Constructs` enclosed among the parentheses. Each group captures a different part of the email address. Local-Part, Domain, Top-level Domain. 

#### Local-Part:

The `([a-z0-9_\.-]*)` would match the username of the email.

This group represents the local part of the email address which ensures that the username follows a valid format.

`example1@test.com`

Local-Part would be `example1` 

#### Domain:

The `([\da-z0-9_\.-])` would match the Domain name.

This group represents the Domain of the email address this helps ensure the domain name follows a valid format.

`example@test.com`

Domain would be `test`

#### Top-Level Domain:

The `([a-z\.]{2,6})` aligns and matches the Top-Level Domain.

This group represents Top-Level Domain of the email address this helps ensure that only valid top-level domains are accepted and matches between 2-6 characters.

`example1@test.com`

Top-Level Domain would be `.com`

### Bracket Expressions
Bracket expressions are fundamental concept in regex, which is used to define a set of characters that can be matched withina single position in a text string. They are denoted by square brackets `[]` and whatever characters enclosed within these brackets will become a part of the set.

In this regex example `/^([a-z0-9_\.-])?@([\da-z0-9_\.-])\.([a-z\.]{2,6})` there are three bracket expressions.

#### Bracket One:
The bracket `[a-z0-9_\.-]` matches any single charaters between `a-z`, `0-9` or one of the characters `_`,`.` or `-`. 

#### Bracket Two: 
The bracket `[\da-z0-9_\.-]` matches any single character in the range `a-z`. `0-9` or one of the characters `.` or `-`.

#### Bracket Three:
The bracket `[a-z\.]{2,6}` matches any single character in the range `a-z` or the literal period character. The expression is then followed by `{2,6}`, which specifies that the matched characters must occur between 2 and 6 times, inclusive. 

In conclusion the regex example `/^([a-z0-9_\.-])?@([\da-z0-9_\.-])\.([a-z\.]{2,6})` matches valid email addresses by using bracket expressions to define character sets for username, domain, and top-level domain.

### Character Classes
Character classes or character sets, are a short and more concise regex that represent specific sets of characters. Using character sets you can simplify regex patterns making them easier to read and understand. 

In this regex example `/^([a-z0-9_\.-])?@([\da-z0-9_\.-])\.([a-z\.]{2,6})` we use various regex elements, including `classes`, `sets`, `metacharacters` and `repeating character classes`. This ensures our regex are processed accurately to match the email address.

#### Character Classes and Character Sets:

In this example `/^([a-z0-9_\.-])?@([\da-z0-9_\.-])\.([a-z\.]{2,6})` we use two primary character classes `/d` and `..`. Character sets are definded in the square brackets `[a-z]`, `[0-9]`, and `[.-]`. These sets represent multiple characters, allowing a single character match from the specified range.

#### Metacharacters:

Metacharacters are characters with special meanings in regex, for example the `(.)` there are situations where some metacharacters can lose their special meaning and would be treated as literals. In the example `[a-z0-9_\.-]` and `[\da-z0-9_\.-]` the dot is escaped with a backslash dot, and the hyphen is used as a literal character, as it is placed at the beginning or end of the character set.

#### Repeating Character Classes:

The email regex uses the `+` and `{2,6}` quantifiers to indicate repeating character classes. The plus sign matches one or more occurrences of the preceding character class or set. For example `/^([a-z0-9_\.-])+` and `[\da-z0-9_\.-]+`. Meaning the curly braces `{2,6}` define a specific range or repetition for the preceding character class or set. 

Thereby, the combination of these elements among our featured regex allows the email to accurately be sources and validated to ensure it matches email addresses

### The OR Operator
The OR operator is an important concpet in regex that defines alternative patterns. The symbol used is `|`, and allows regex to match either one pattern or another.

For example `^(Self Driving Cars| Autonomous Cars)$` matches either the string `Self Driving Cars` or `Autonomous Cars` but won't be able to match both or other strings.

Crucial for functioning with regex, the OR operator allows for creation of flexible patterns.

### Flags
Flags are modifiers which affect the behavior of regular expressions(regex) by enabling or disabling certain features and are appended to the end of the regex pattern, outside the slashes. Flags are used to control case sensitivity, multiline matching, and global matching.

### Character Escapes
Character escapes are an essential aspect of regex, enabling precise pattern matching by treating metacharacters as literal characters and representing non-typable characters. 

#### Backslash:

The backslash is a common escape character used to treat metacharacters as literals in regex. In our example previously used the dot `.` is escaped with a backslash `[\da-z0-9_\.-]`. Ensuring the dot is treated as a literal period. 

#### Metacharaters:

Metacharacters have important meaning in regex. The `.`,`+`,`^` when placed among character classes, they often lose their meanings and behave as though they are regular charaters. The `-` in our example `[\da-z0-9_\.-]` is used as a literal character inside the character class without needing to be escaped.

#### Escape Sequences:

Escape sequences, are characters that can't be directly typed in a string, so they are implemented then used. The sequences are started with a `\` then followed by a combination or letters. In our example the `\d` is an escape sequence that represents any digit from 0-9, shortening `[0-9]`

## Author

[Leon Hoti](https://github.com/Leonn24)
[Deployed GitHub-Gist Link: Click Here](https://gist.github.com/Leonn24/573032ef7b89bc003c4d0c81b6dc031f)
[Deployed GitHub Repo Link: Click Here](https://github.com/Leonn24/regexguide)