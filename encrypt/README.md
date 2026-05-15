# 🔐 CipherDeck — Caesar + Vigenere Cipher Tool

> A zero-dependency, browser-based classical cryptography tool with real-time visualisation.

![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)
![HTML5](https://img.shields.io/badge/HTML5-%23E34F26.svg?logo=html5&logoColor=white)
![Vanilla JS](https://img.shields.io/badge/JavaScript-ES6+-yellow.svg?logo=javascript)

---

## ✨ Features

- **Caesar cipher** — fixed alphabetic shift (ROT-N), shift 1–25 via slider
- **Vigenere cipher** — keyword-driven polyalphabetic substitution
- **Encrypt / Decrypt** — toggle with one click
- **Live alphabet strip** — visualises the Caesar shift mapping (A→Z plaintext vs cipher)
- **Character mapping chips** — shows up to 12 unique letter substitutions from your text
- **Copy to clipboard** — one-click copy of cipher output
- **Zero dependencies** — pure HTML + CSS + JS, no build step

---

## 📁 Project Structure

```text
cipher-tool/
│
├── index.html      ← Entire application (HTML + CSS + JS)
└── README.md       ← This file
```

All code lives in `index.html`, split into clearly labelled comment sections.

---

## 🔬 How the Ciphers Work

### Caesar Cipher

Each letter is rotated by a fixed shift `N` (1–25).

```text
Encrypt:  C = (P + N)      mod 26
Decrypt:  P = (C - N + 26) mod 26
```

| Plain  | A | B | C | … | Z |
|--------|---|---|---|---|---|
| Shift 3 (Caesar's original) | D | E | F | … | C |

Non-alphabetic characters (spaces, digits, punctuation) are passed through unchanged.  
Case is preserved — uppercase encrypts to uppercase, lowercase to lowercase.

---

### Vigenere Cipher

Each letter is shifted by the value of the corresponding keyword character (A=0, B=1, … Z=25).  
The keyword repeats cyclically. Only alphabetic characters consume a key position.

```text
Encrypt:  C[i] = (P[i] + K[i mod len(K)])       mod 26
Decrypt:  P[i] = (C[i] - K[i mod len(K)] + 26)  mod 26
```

**Example** — keyword `KEY`, plaintext `HELLO`:

| Plaintext  | H  | E  | L  | L  | O  |
|------------|----|----|----|----|-----|
| Key char   | K  | E  | Y  | K  | E  |
| Shift      | 10 | 4  | 24 | 10 | 4  |
| Ciphertext | R  | I  | J  | V  | S  |

---

## 🗂️ Code Comment Style

Every section uses a banner comment:

```js
// ─────────────────────────────────────────────
// 3. CAESAR CIPHER
//
// Formula (encrypt): C = (P + shift) mod 26
// Formula (decrypt): P = (C - shift + 26) mod 26
// ─────────────────────────────────────────────
```

Functions use JSDoc:

```js
/**
 * caesarChar — shift a single character by `shift` positions.
 * @param {string}  ch    - a single character
 * @param {number}  shift - shift amount (1–25)
 * @param {boolean} enc   - true = encrypt, false = decrypt
 * @returns {string} transformed character
 */
function caesarChar(ch, shift, enc) { ... }
```

Inline comments explain *why*, not *what*:

```js
// Non-alpha: pass through, do NOT advance key index
if (!isUpper && !isLower) return { out: ch, consumed: false };
```

---

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/cipher-tool.git
cd cipher-tool
open index.html   # or xdg-open / start on Linux / Windows
```

No `npm install`. No server. Just open and run. ✅

---

## 🔧 Extending

Add a new cipher by following this pattern in `script`:

```js
// 1. Write an encoder/decoder function
function rot13Text(text, enc) { ... }

// 2. Add a tab pill in HTML
// <button class="tab-pill" onclick="setTab('rot13')">ROT-13</button>

// 3. Handle the new tab in setTab() and run()
```

---

## ♿ Accessibility

- `role="tab"` + `aria-selected` on cipher selector pills
- `aria-pressed` on encrypt/decrypt buttons
- `aria-live="polite"` on output + shift badge
- Keyboard navigable — Tab, Enter, Space (+ Arrow keys on tab pills)

---

## 📄 License

MIT © 2026 Your Name
