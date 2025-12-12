# The 20% of Regex That Covers 80% of Use Cases - Enhanced Guide

## Introduction: What is Regex and Why Learn It?

Regular expressions (regex) are patterns used to match character combinations in strings. Think of them as a powerful "find and replace" on steroids. You'll use regex for:

- **Data validation** (emails, phone numbers, passwords)
- **Text parsing** (extracting information from logs, documents)
- **Search and replace** (cleaning data, reformatting text)
- **Web scraping** (finding patterns in HTML)

---

## 1. Basic Character Matching

### The Dot `.` - Your Wildcard Character

**`.`** - Matches any single character (except newline by default)

**Use Cases:**

- Matching patterns where one character varies
- Finding typos or variations in text
- Template matching with unknown characters

**Examples:**

```
Pattern: a.c
Matches: "abc", "a5c", "a@c", "a c"
Does NOT match: "ac" (needs exactly one character between)

Pattern: file.txt
Matches: "file1.txt", "file2.txt", "fileA.txt"
Use: Finding numbered file variations
```

**⚠️ Common Catch:** The dot is TOO powerful - it matches everything! If you actually want to match a literal period/dot, you must escape it: `\.`

```
Pattern: 3.14  (WRONG - matches "3X14", "3.14", "3a14")
Pattern: 3\.14 (CORRECT - matches only "3.14")
```

**💡 Pro Tip:** When matching file extensions, always escape the dot:

```
Wrong: .jpg (matches "Xjpg", " jpg")
Right: \.jpg (matches only ".jpg")
```

---

### Digit Matching `\d`

**`\d`** - Matches any digit (0-9)

**Use Cases:**

- Extracting numbers from text
- Validating numeric input
- Parsing dates and times
- Finding quantities in documents

**Examples:**

```
Pattern: \d
Matches: Any single digit "5", "0", "9"

Pattern: \d\d\d
Matches: "123", "456", "007"
Use: Area codes, PIN codes

Pattern: Room \d\d\d
Matches: "Room 405", "Room 102"
Use: Hotel room numbers, office numbers
```

**Real-World Example:**

```
Text: "I bought 3 apples for $2.50"
Pattern: \d
Matches: "3", "2", "5", "0" (each digit separately)
```

**⚠️ Common Catch:** `\d` only matches single digits. To match multi-digit numbers, you need quantifiers (covered next).

---

### Word Character `\w`

**`\w`** - Matches any word character (letters a-z, A-Z, digits 0-9, underscore _)

**Use Cases:**

- Matching variable names in code
- Extracting usernames
- Parsing identifiers
- Matching words without spaces

**Examples:**

```
Pattern: \w
Matches: "a", "Z", "5", "_"
Does NOT match: " ", "@", "-", "."

Pattern: user_\w\w\w
Matches: "user_123", "user_abc", "user_5a_"
Use: Database naming conventions
```

**⚠️ Common Catch:** `\w` does NOT match hyphens or most special characters!

```
Pattern: \w (won't match the hyphen in "co-worker")
```

**💡 Pro Tip:** Remember the mnemonic "word, digit, underscore" for `\w`

---

### Whitespace `\s`

**`\s`** - Matches any whitespace (space, tab `\t`, newline `\n`, carriage return `\r`)

**Use Cases:**

- Cleaning up extra spaces
- Parsing indented text
- Splitting words
- Normalizing whitespace in data

**Examples:**

```
Pattern: \s
Matches: " " (space), "\t" (tab), "\n" (newline)

Pattern: hello\sworld
Matches: "hello world", "hello\tworld", "hello\nworld"
```

**Real-World Example:**

```
Text: "hello     world" (multiple spaces)
Pattern: \s\s+ (match 2 or more spaces)
Use: Finding extra whitespace to clean up
```

---

### Negations: The Opposite Matchers

**`\D`** - Matches any NON-digit **`\W`** - Matches any NON-word character  
**`\S`** - Matches any NON-whitespace

**Use Cases:**

- Validating that text contains no numbers
- Finding punctuation and special characters
- Extracting non-space content

**Examples:**

```
Pattern: \D
Matches: "a", "@", " ", "Z"
Does NOT match: "0", "5", "9"

Pattern: \W
Matches: " ", "@", "-", ".", "!"
Use: Finding punctuation or special characters

Pattern: \S
Matches: Any visible character (letters, numbers, symbols)
Use: Finding non-empty content
```

**Real-World Example:**

```
Text: "Error on line 42: Invalid input"
Pattern: \D+ (one or more non-digits)
Extracts: "Error on line ", ": Invalid input"
```

---

## 2. Quantifiers (How Many Times)

Quantifiers tell regex HOW MANY of the preceding character/pattern to match.

### Zero or More `*`

**`*`** - Matches 0 or more occurrences

**Use Cases:**

- Optional repeated characters
- Matching variable-length patterns
- Flexible string matching

**Examples:**

```
Pattern: ab*c
Matches: "ac" (zero b's), "abc" (one b), "abbbc" (many b's)

Pattern: \d*
Matches: "" (empty), "5", "123", "999999"
Use: Optional numbers
```

**Real-World Example:**

```
Pattern: https*://
Matches: "http://example.com" AND "https://example.com"
Use: Matching both HTTP and HTTPS URLs
```

**⚠️ Common Catch:** `*` can match NOTHING (zero occurrences)! This can lead to unexpected empty matches.

```
Text: "hello"
Pattern: x*
Matches: Empty string at EVERY position (before h, between letters, after o)
```

**💡 Pro Tip:** If you need AT LEAST ONE match, use `+` instead of `*`

---

### One or More `+`

**`+`** - Matches 1 or more occurrences (must appear at least once)

**Use Cases:**

- Matching sequences that must exist
- Extracting repeated patterns
- Finding runs of characters

**Examples:**

```
Pattern: ab+c
Matches: "abc", "abbbbc"
Does NOT match: "ac" (requires at least one b)

Pattern: \d+
Matches: "5", "123", "999999"
Does NOT match: "" (empty string)
Use: Extracting whole numbers
```

**Real-World Examples:**

```
Pattern: \s+
Use: Match one or more spaces/whitespace
Application: Find all whitespace runs to replace with single space

Pattern: [A-Z]+
Matches: "USA", "NASA", "HTML"
Use: Finding acronyms

Pattern: \w+
Matches: "hello", "test_123", "variable_name"
Use: Extracting complete words or identifiers
```

**⚠️ Common Catch:** `+` is greedy by default - it matches as much as possible!

```
Text: "aaaa"
Pattern: a+
Matches: "aaaa" (all four a's, not just one)
```

---

### Optional `?`

**`?`** - Matches 0 or 1 occurrence (makes preceding element optional)

**Use Cases:**

- Handling spelling variations
- Optional formatting characters
- Flexible pattern matching

**Examples:**

```
Pattern: colou?r
Matches: "color" AND "colour"
Use: Handling US vs UK spelling

Pattern: -?\d+
Matches: "42" AND "-42"
Use: Matching positive or negative numbers

Pattern: https?://
Matches: "http://" AND "https://"
```

**Real-World Examples:**

```
Pattern: Mr\.? Smith
Matches: "Mr Smith" AND "Mr. Smith"
Use: Handling optional punctuation

Pattern: \(?\d{3}\)?
Matches: "(123)" AND "123"
Use: Phone numbers with optional parentheses

Pattern: files?
Matches: "file" AND "files"
Use: Handling singular/plural
```

**💡 Pro Tip:** The `?` makes things optional, but it's also used for non-greedy matching (covered later)

---

### Specific Counts `{n,m}`

**`{n}`** - Exactly n times **`{n,}`** - n or more times **`{n,m}`** - Between n and m times

**Use Cases:**

- Fixed-length codes (ZIP, PIN)
- Constrained input validation
- Precise pattern matching

**Examples:**

```
Pattern: \d{3}
Matches: "123", "456", "007"
Does NOT match: "12" or "1234"
Use: Exactly 3 digits (area codes, CVV codes)

Pattern: \d{3,5}
Matches: "123", "1234", "12345"
Does NOT match: "12" or "123456"
Use: Between 3 and 5 digits

Pattern: \d{4,}
Matches: "1234", "12345", "123456789"
Does NOT match: "123"
Use: At least 4 digits
```

**Real-World Examples:**

```
Pattern: \d{5}
Use: US ZIP codes
Matches: "90210", "10001"

Pattern: \d{3}-\d{2}-\d{4}
Use: Social Security Numbers
Matches: "123-45-6789"

Pattern: [A-Z]{2,3}
Use: State/country codes
Matches: "CA", "USA", "UK"

Pattern: \w{8,}
Use: Password minimum length (8+ characters)
Matches: "password123", "secure_pass"
```

**⚠️ Common Catch:** Ranges are inclusive! `{3,5}` means 3, 4, OR 5 - not "up to 5".

**💡 Pro Tip:** Use `{n}` when you know the exact count (phone numbers, codes). Use `{n,m}` for flexible validation.

---

## 3. Character Sets

Character sets let you match ANY ONE character from a group.

### Basic Character Sets `[abc]`

**`[abc]`** - Matches any single character inside the brackets

**Use Cases:**

- Matching specific options
- Vowel/consonant matching
- Flexible character matching

**Examples:**

```
Pattern: [aeiou]
Matches: Any single vowel
In "hello": matches "e", "o"

Pattern: [0-9]
Matches: Any single digit (same as \d)

Pattern: [a-z]
Matches: Any lowercase letter

Pattern: [a-zA-Z]
Matches: Any letter (upper or lower)

Pattern: [a-zA-Z0-9]
Matches: Any letter or digit (similar to \w, but no underscore)
```

**Real-World Examples:**

```
Pattern: [Yy]es
Matches: "Yes" OR "yes"
Use: Case-insensitive matching

Pattern: [0-9][0-9][0-9]
Matches: Any 3-digit number
Same as: \d{3}

Pattern: [A-F0-9]
Matches: Hexadecimal digits
Use: Color codes, memory addresses

Pattern: gr[ae]y
Matches: "gray" AND "grey"
Use: Spelling variations
```

**⚠️ Common Catch:** Inside brackets, most special characters lose their meaning!

```
[.+*] matches literal ".", "+", or "*" (not their regex meanings)
[a-z] is a RANGE, but [az-] matches "a", "z", or "-"
```

**💡 Pro Tip:** Order matters for ranges: `[a-z]` works, but `[z-a]` is an error!

---

### Negated Character Sets `[^abc]`

**`[^abc]`** - Matches anything NOT in the brackets

**Use Cases:**

- Excluding specific characters
- Matching "everything except"
- Validation rules

**Examples:**

```
Pattern: [^0-9]
Matches: Any non-digit
Same as: \D

Pattern: [^aeiou]
Matches: Any consonant (or non-letter)

Pattern: [^\s]
Matches: Any non-whitespace
Same as: \S
```

**Real-World Examples:**

```
Pattern: [^,]+
Matches: Everything up to a comma
Use: Parsing CSV fields

Pattern: [^@]+@[^@]+
Matches: Simple email pattern (everything except @ on both sides)
Use: Basic email validation

Pattern: [^<>]+
Matches: Text outside HTML tags
Use: Extracting plain text from HTML

Pattern: [^a-zA-Z]
Matches: Anything that's not a letter
Use: Finding special characters and numbers
```

**⚠️ Common Catch:** The `^` inside brackets means "NOT", but outside brackets it means "start of line"!

```
[^abc] - matches anything except a, b, c
^[abc] - matches a, b, or c at the START of the string
```

---

## 4. Anchors (Position Matching)

Anchors don't match characters - they match POSITIONS in the text.

### Start of String `^`

**`^`** - Matches the start of a string/line

**Use Cases:**

- Validating string format from the beginning
- Ensuring strings start with specific patterns
- Line-by-line processing

**Examples:**

```
Pattern: ^Hello
Matches: "Hello world"
Does NOT match: "Say Hello" (Hello not at start)

Pattern: ^\d+
Matches: Lines starting with numbers
In "123 Main St": matches "123"
In "Main St 123": no match
```

**Real-World Examples:**

```
Pattern: ^#
Use: Finding comments in code (lines starting with #)
Matches: "# This is a comment"

Pattern: ^https://
Use: Validating URL starts with https
Matches: "https://example.com"

Pattern: ^[A-Z]
Use: Ensuring text starts with capital letter
Matches: "Hello" but not "hello"

Pattern: ^\s*$
Use: Finding empty lines (with optional whitespace)
Matches: "", "   ", "\t"
```

**💡 Pro Tip:** In multiline mode, `^` matches the start of each line, not just the string.

---

### End of String `$`

**`$`** - Matches the end of a string/line

**Use Cases:**

- Validating string format at the end
- File extension checking
- Ensuring complete pattern matching

**Examples:**

```
Pattern: world$
Matches: "Hello world"
Does NOT match: "world peace" (world not at end)

Pattern: \d+$
Matches: Lines ending with numbers
In "Order #123": matches "123"
```

**Real-World Examples:**

```
Pattern: \.txt$
Use: Finding text files
Matches: "document.txt", "file.txt"
Does NOT match: "text.doc", "readme.txt.bak"

Pattern: [.!?]$
Use: Checking if sentence ends with punctuation
Matches: "Hello!", "Really?"

Pattern: ^\d+$
Use: Ensuring string contains ONLY digits
Matches: "12345" (entire string is digits)
Does NOT match: "123abc", "abc123"
```

**⚠️ Common Catch:** Combining `^` and `$` means the ENTIRE string must match!

```
Pattern: ^\d{3}$
Matches: "123" (exactly 3 digits, nothing else)
Does NOT match: "1234", "abc123", "123abc"
```

---

### Word Boundary `\b`

**`\b`** - Matches a word boundary (between word and non-word character)

**Use Cases:**

- Finding whole words only
- Avoiding partial matches
- Precise word searching

**Examples:**

```
Pattern: \bcat\b
Matches: "the cat sat"
Does NOT match: "category", "scat", "concatenate"

Pattern: \btest\b
Matches: "test", "a test here"
Does NOT match: "testing", "contest", "attest"
```

**Real-World Examples:**

```
Pattern: \b\d{3}\b
Use: Finding 3-digit numbers as separate words
Matches: "I have 123 items"
Does NOT match: "1234" or "the12345"

Pattern: \b[A-Z]{2,}\b
Use: Finding acronyms (2+ capital letters as whole words)
Matches: "NASA", "FBI", "HTML"
Does NOT match: "SomeName", "HTMLElement"

Pattern: \bthe\b
Use: Finding the word "the" (not "there", "them")
Case sensitive: won't match "The"

Pattern: \b\w+@\w+\.\w+\b
Use: Simple email extraction (whole words only)
```

**⚠️ Common Catch:** Underscores are word characters!

```
Pattern: \btest\b
Does NOT match: "my_test_function" (underscore is part of word)
```

**💡 Pro Tip:** Use `\B` for NON-word boundary (opposite of `\b`)

```
Pattern: \Bion\B
Matches: "nation" (ion in the middle)
Does NOT match: "ion" (standalone) or "lion" (at end)
```

---

## 5. Groups and Alternation

### Capture Groups `()`

**`()`** - Creates a capture group (captures matched text for extraction)

**Use Cases:**

- Extracting specific parts of a match
- Grouping patterns together
- Backreferences (referring to captured groups)
- Applying quantifiers to multiple characters

**Examples:**

```
Pattern: (\d{3})-(\d{4})
Matches: "555-1234"
Captures: Group 1 = "555", Group 2 = "1234"
Use: Separating phone number parts

Pattern: (ha)+
Matches: "ha", "haha", "hahaha"
Use: Quantifier applies to entire group

Pattern: (\w+)@(\w+)\.(\w+)
Matches: "user@example.com"
Captures: Group 1 = "user", Group 2 = "example", Group 3 = "com"
```

**Real-World Examples:**

```
Pattern: ^(.+)@(.+)$
Use: Email extraction - split username and domain
Input: "john.doe@company.com"
Group 1: "john.doe"
Group 2: "company.com"

Pattern: (\d{2})/(\d{2})/(\d{4})
Use: Date parsing
Input: "12/31/2024"
Group 1: "12" (month)
Group 2: "31" (day)
Group 3: "2024" (year)

Pattern: (Mr|Mrs|Ms)\.? (\w+)
Use: Parsing names with titles
Input: "Mrs. Smith"
Group 1: "Mrs"
Group 2: "Smith"

Pattern: <(\w+)>.*?</\1>
Use: Matching HTML tags (with backreference \1)
Matches: "<div>content</div>"
Group 1: "div", \1 refers back to same tag name
```

**⚠️ Common Catch:** Groups are numbered left-to-right by opening parenthesis!

```
Pattern: ((\d{3})-(\d{4}))
Group 1: entire match "555-1234"
Group 2: "555"
Group 3: "1234"
```

**💡 Pro Tip:** Use non-capturing groups `(?:...)` when you need grouping but don't need to extract:

```
Pattern: (?:ha)+
Matches: "haha" but doesn't create a capture group (saves memory)
```

---

### Alternation `|`

**`|`** - OR operator (matches either pattern)

**Use Cases:**

- Multiple valid options
- Spelling variations
- Format alternatives

**Examples:**

```
Pattern: cat|dog
Matches: "cat" OR "dog"

Pattern: jpg|png|gif
Matches: Any of these image extensions

Pattern: yes|no
Matches: "yes" OR "no"
```

**Real-World Examples:**

```
Pattern: \.(jpg|jpeg|png|gif)$
Use: Matching image files
Matches: "photo.jpg", "image.png", "pic.gif"

Pattern: (Mr|Mrs|Ms|Dr)\.
Use: Title matching
Matches: "Mr.", "Dr.", etc.

Pattern: https?://|www\.
Use: Finding URLs (with or without protocol)
Matches: "https://site.com", "www.example.com"

Pattern: \b(0[1-9]|1[0-2])/\d{2}/\d{4}\b
Use: Month validation in dates (01-12)
Matches: "01/15/2024", "12/31/2024"
Does NOT match: "13/15/2024", "00/01/2024"

Pattern: true|false|null
Use: JSON value validation
```

**⚠️ Common Catch:** Order matters! Alternation tries patterns left-to-right and stops at first match.

```
Pattern: cat|category
In "category": matches "cat" (stops there)

Better: category|cat
In "category": matches "category" (longer match first)
```

**💡 Pro Tip:** Use grouping with alternation for clarity:

```
Pattern: file.(txt|doc)
Matches: "file.txt", "file.doc"

Pattern: (red|blue|green) car
Matches: "red car", "blue car", "green car"
```

---

## 6. Greedy vs Non-Greedy Matching

By default, quantifiers (`*`, `+`, `?`) are GREEDY - they match as much text as possible.

### Greedy Matching (Default)

**Examples:**

```
Text: "<b>Hello</b> <i>World</i>"
Pattern: <.*>
Matches: "<b>Hello</b> <i>World</i>" (entire string!)
Why: .* matches everything including "> <" between tags

Text: "aaaa"
Pattern: a+
Matches: "aaaa" (all four, not just one)

Text: 'He said "hello" and "goodbye"'
Pattern: ".*"
Matches: '"hello" and "goodbye"' (from first to last quote)
```

**⚠️ The Problem:** Greedy matching often matches MORE than you want!

---

### Non-Greedy Matching

**`*?`** - 0 or more (non-greedy) **`+?`** - 1 or more (non-greedy) **`??`** - 0 or 1 (non-greedy)

The `?` after a quantifier makes it match as LITTLE as possible.

**Examples:**

```
Text: "<b>Hello</b> <i>World</i>"
Pattern: <.*?>
Matches: "<b>", "</b>", "<i>", "</i>" (each tag separately)

Text: "aaaa"
Pattern: a+?
Matches: "a" (just one, though more are available)

Text: 'He said "hello" and "goodbye"'
Pattern: ".*?"
Matches: "hello" and "goodbye" (each quoted string separately)
```

**Real-World Examples:**

```
Pattern: \[.*?\]
Use: Extracting bracketed content
Text: "[first] some text [second]"
Greedy: matches "[first] some text [second]" (entire string)
Non-greedy: matches "[first]" and "[second]" (separately)

Pattern: <(\w+)>.*?</\1>
Use: Matching HTML tags with content
Text: "<p>Hello</p><p>World</p>"
Matches: "<p>Hello</p>" and "<p>World</p>" (each tag pair)

Pattern: /\*.*?\*/
Use: Matching C-style comments
Text: "/* comment 1 */ code /* comment 2 */"
Matches: "/* comment 1 */" and "/* comment 2 */" (each comment)

Pattern: \{.*?\}
Use: Extracting JSON objects
Text: '{"a":1} text {"b":2}'
Matches: '{"a":1}' and '{"b":2}' (each object)
```

**💡 Pro Tip:** When matching between delimiters (quotes, brackets, tags), ALWAYS use non-greedy:

```
Right: <.*?>  - matches individual tags
Wrong: <.*>   - matches from first < to last >
```

---

## 10 Real-World Examples You'll Use Constantly

### 1. Email Validation (Simple)

```
\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b

Breaking it down:
\b                    - Word boundary (start)
[A-Za-z0-9._%+-]+    - Username (letters, numbers, dots, etc.)
@                     - Literal @ symbol
[A-Za-z0-9.-]+       - Domain name
\.                    - Literal dot (escaped)
[A-Za-z]{2,}         - Extension (at least 2 letters)
\b                    - Word boundary (end)

Matches: "user@example.com", "test.user@my-site.org"
Doesn't match: "invalid@", "@example.com", "no-at-sign.com"

⚠️ Note: This is simplified. Real email validation is extremely complex!
```

### 2. Phone Number (US Format)

```
\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}

Breaking it down:
\(?       - Optional opening parenthesis
\d{3}     - 3 digits (area code)
\)?       - Optional closing parenthesis
[-.\s]?   - Optional separator (dash, dot, or space)
\d{3}     - 3 digits
[-.\s]?   - Optional separator
\d{4}     - 4 digits

Matches: "(123) 456-7890", "123-456-7890", "123.456.7890", "1234567890"

💡 Tip: Add ^ and $ to ensure entire string matches:
^\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}$
```

### 3. URL Matching

```
https?://[^\s]+

Breaking it down:
https?    - http or https (s is optional)
://       - Literal ://
[^\s]+    - One or more non-whitespace characters

Matches: "http://example.com", "https://site.com/path?query=1"
Use: Finding URLs in text, log files

More robust version:
https?://[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}(/[^\s]*)?
```

### 4. Extract Numbers from Text

```
\d+\.?\d*

Breaking it down:
\d+      - One or more digits (integer part)
\.?      - Optional decimal point
\d*      - Zero or more digits (fractional part)

Matches: "123", "45.67", "0.5", "99"
Use: Extracting prices, measurements, quantities

Example:
Text: "Price: $19.99, Quantity: 5"
Extracts: "19.99", "5"
```

### 5. Remove Extra Whitespace

```
Find: \s+
Replace with: (single space)

Breaking it down:
\s+    - One or more whitespace characters (spaces, tabs, newlines)

Use: Cleaning up messy text formatting
Before: "hello    world\t\tthere"
After:  "hello world there"

Advanced: Remove leading/trailing whitespace
Find: ^\s+|\s+$
Replace with: (empty)
```

### 6. Extract Hashtags

```
#\w+

Breaking it down:
#      - Literal hashtag symbol
\w+    - One or more word characters (letters, digits, underscore)

Matches: "#coding", "#javascript", "#AI_ML"
Use: Social media parsing, sentiment analysis

More robust (handle underscores properly):
#[A-Za-z0-9_]+

With word boundary to avoid partial matches:
\B#\w+\b
```

### 7. Date Matching (MM/DD/YYYY or MM-DD-YYYY)

```
\d{2}[/-]\d{2}[/-]\d{4}

Breaking it down:
\d{2}     - 2 digits (month)
[/-]      - Slash or dash
\d{2}     - 2 digits (day)
[/-]      - Slash or dash
\d{4}     - 4 digits (year)

Matches: "12/31/2024", "01-15-2024"
Doesn't validate: "99/99/9999" (still matches syntactically)

With validation (months 01-12):
(0[1-9]|1[0-2])[/-](0[1-9]|[12][0-9]|3[01])[/-]\d{4}
```

### 8. Password Validation (8+ chars, letter + number)

```
^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$

Breaking it down:
^                  - Start of string
(?=.*[A-Za-z])    - Lookahead: must contain at least one letter
(?=.*\d)          - Lookahead: must contain at least one digit
[A-Za-z\d]{8,}    - 8 or more letters/digits
$                  - End of string

Matches: "password123", "12345abc", "SecurePass1"
Doesn't match: "password" (no digit), "12345678" (no letter), "Pass1" (too short)

With special character requirement:
^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$
```

### 9. File Extensions

```
\.(jpg|png|gif|pdf|docx?)$

Breaking it down:
\.          - Literal dot (escaped)
(...)       - Group of alternatives
jpg|png|... - Various extensions
docx?       - doc or docx (x is optional)
$           - End of string

Matches: "photo.jpg", "report.pdf", "file.docx", "old.doc"
Use: File filtering, upload validation

Case-insensitive version:
\.(jpe?g|png|gif|pdf|docx?)$
Matches: "IMG.JPG", "Photo.Png"
```

### 10. IP Address (Simple)

```
\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b

Breaking it down:
\b             - Word boundary
\d{1,3}        - 1 to 3 digits
\.             - Literal dot
(repeat 4 times)
\b             - Word boundary

Matches: "192.168.1.1", "10.0.0.1"
Doesn't validate: "999.999.999.999" (syntactically correct but invalid IP)

With validation (0-255 per octet):
\b(25[0-5
```
