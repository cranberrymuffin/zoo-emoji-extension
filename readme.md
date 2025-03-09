# Animal Emoji Replacer

This is a simple JavaScript tool that automatically replaces specified animal names in the text content of a webpage with their corresponding emojis. It uses the `TreeWalker` API to traverse the DOM and applies regular expressions to replace matched words with emojis.

## Features

- Replaces animal names in the text with their respective animal emojis.
- Supports both singular and plural forms of animal names.
- Works on all text content within the body of the webpage (e.g., paragraphs, headings, list items).
- Written in vanilla JavaScript with no external dependencies.

## How It Works

### Step 1: Define Animal Names and Emojis

A predefined list (`whatToReplace`) contains animal names and their corresponding emojis. The list includes common animals such as dogs, cats, rabbits, and more.

```javascript
const whatToReplace = [
  [/\bdog(s?)\b/gi, "🐶$1"],
  [/\bcat(s?)\b/gi, "🐱$1"],
  [/\bmouse(s?)\b/gi, "🐭$1"],
  ...
];
```

Each entry in the list is a regular expression paired with the emoji replacement. The `s?` in the regex ensures the code matches both singular and plural forms of the animal names (e.g., "dog" and "dogs").

### Step 2: Traverse the DOM

A `TreeWalker` is used to traverse the text nodes of the webpage. This ensures only text content (not HTML elements or attributes) is processed.

```javascript
const walk = document.createTreeWalker(
  document.body,
  NodeFilter.SHOW_TEXT,
  null,
  false
);
```

### Step 3: Apply the Replacements

For each text node, the script iterates through the `whatToReplace` list, replacing any matches with the corresponding emoji.

```javascript
let node;
while ((node = walk.nextNode())) {
  for (let [rx, replacement] of whatToReplace) {
    node.nodeValue = node.nodeValue.replace(rx, replacement);
  }
}
```

This step ensures that all specified animal names are replaced with emojis in the visible text content of the page.

### Example

Before:

```
The dog and the cat are friends.
```

After:

```
The 🐶 and the 🐱 are friends.
```

## Customization

You can easily extend or modify the list of animal names and emojis by updating the `whatToReplace` array. Just add or remove entries as needed.

```javascript
const whatToReplace = [
  [/\bdog(s?)\b/gi, "🐶$1"],
  [/\bcat(s?)\b/gi, "🐱$1"],
  [/\bfish(es?)\b/gi, "🐟$1"],
  ...
];
```

## Contributions

Feel free to fork this repository, open issues, and submit pull requests. Contributions are welcome!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
