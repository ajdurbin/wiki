# Usage #
- `grep regex file`
- `grep -i regex file` is case insensitive matching
- Python `re` module

# Metacharacter Reference #
- `*`: Match anything, eg, `*.txt$` matches anything that ends in `.txt`.
- `?`: Optional match a character, eg, `?at` matches all of 'cat', 'rat', 'sat', `at`, etc.
- `^`: Start of a line. Or negation inside `[^abc]`
- `$`: End of a line.
- `[..]`: Character class. Explicitly list the characters we want to match, eg, `[aeiou]` matches any vowels, `[A-Za-z]` matches any alphabetical character, `[0-9]` matches any digit, `[^ae]` matches everything but 'a' or 'e'. Note that `-` inside a character class is only considered a character if it's first.
- `.` matches any single character.
- `|` means 'or' and is often used with parentheses to constrain the alternation, eg, `gr(a|e)y`. Note that `gr[a|e]y` is not valid because `|` is interpreted as a character and not a metacharacter inside brackets, also `gr[ae]y` works.
- `\<word\>` are word boundary metacharacters, this example matches 'word' and not 'stopwords'.
- `+` matches one or more of the immediately preceding item.

# Alternation Versus Character Class #

While `gr[ae]y` and `gr(a|e)y` are equivalent, character classes only match single characters. Using alternation, we can match full words, eg, `^(From|Subject):` matches either of those words.
