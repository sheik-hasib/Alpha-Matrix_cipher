# 🔐 AlphaMatrix Cipher (AMC)

## 👨‍🎓 Submitted By:
- **Name:** YOUR NAME  
- **ID:** YOUR ID  
- **Department:** YOUR DEPT  

## 📘 Course Info:
- **Course Title:** Cryptography & Security  
- **Instructor:** YOUR INSTRUCTOR NAME  

---

## 📌 Algorithm Name: AlphaMatrix Cipher (AMC)

A custom-built mathematical encryption system based on character position and letter-to-number mapping.

---

## 🧠 Concept Overview:
- Characters from **a to z** and **A to Z** are mapped as numbers from **0 to 25**.
- Encryption applies a transformation using the formula `C[i] = (P[i] + K + i²) % 26`.
- Decryption reverses the formula to recover the original character.
- **Case sensitivity** is preserved.
- **Non-letter characters** remain unchanged.

---

## 🔐 Encryption Algorithm (Pseudocode + Math)

**Input:** Plaintext `P` (a-z, A-Z), Integer Key `K`  
**Output:** Ciphertext `C`

```pseudocode
For i = 0 to length(P)-1:
    If P[i] is a letter:
        base = 'a' if lowercase else 'A'
        Pn = ASCII(P[i]) - base
        Cn = (Pn + K + i^2) % 26
        C[i] = base + Cn
    Else:
        C[i] = P[i] // non-letters unchanged
Return C
```

**Mathematical Formula:**
```
C[i] = ( P[i] + K + i² ) mod 26
```

---

## 🔓 Decryption Algorithm (Pseudocode + Math)

**Input:** Ciphertext `C`, Integer Key `K`  
**Output:** Plaintext `P`

```pseudocode
For i = 0 to length(C)-1:
    If C[i] is a letter:
        base = 'a' if lowercase else 'A'
        Cn = ASCII(C[i]) - base
        Pn = (Cn - K - i^2 + 26) % 26
        P[i] = base + Pn
    Else:
        P[i] = C[i] // non-letters unchanged
Return P
```

**Mathematical Formula:**
```
P[i] = ( C[i] - K - i² + 26 ) mod 26
```

---

## 🔄 Flowchart Description

### 🔐 Encryption Flow:
```
[Start]
   |
   v
[Input plaintext and key]
   |
   v
[For each character in plaintext]
   |--> If letter: convert to 0-25 (a/A = 0)
   |--> Compute C[i] = (P[i] + K + i²) % 26
   |--> Preserve case and convert to letter
   |--> Else: keep unchanged
   |
   v
[Output Ciphertext]
   |
   v
[End]
```

### 🔓 Decryption Flow:
```
[Start]
   |
   v
[Input ciphertext and key]
   |
   v
[For each character in ciphertext]
   |--> If letter: convert to 0-25 (a/A = 0)
   |--> Compute P[i] = (C[i] - K - i² + 26) % 26
   |--> Preserve case and convert to letter
   |--> Else: keep unchanged
   |
   v
[Output Plaintext]
   |
   v
[End]
```

---

## 🧪 Experimental Test Case

- **Plaintext:** `HeLLo123`  
- **Key:** `3`  
- **Encrypted:** `KiSXh123`  
- **Decrypted:** `HeLLo123`

---

## 🧑‍💻 Source Code: `alpha_matrix_cipher.c`

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int charToNum(char ch) {
    return isupper(ch) ? ch - 'A' : ch - 'a';
}

char numToChar(int num, char original) {
    return isupper(original) ? 'A' + num : 'a' + num;
}

void encrypt(char *plaintext, char *ciphertext, int key) {
    int i;
    for (i = 0; i < strlen(plaintext); i++) {
        char ch = plaintext[i];
        if (isalpha(ch)) {
            int p = charToNum(ch);
            int c = (p + key + (i * i)) % 26;
            ciphertext[i] = numToChar(c, ch);
        } else {
            ciphertext[i] = ch;
        }
    }
    ciphertext[i] = '\0';
}

void decrypt(char *ciphertext, char *plaintext, int key) {
    int i;
    for (i = 0; i < strlen(ciphertext); i++) {
        char ch = ciphertext[i];
        if (isalpha(ch)) {
            int c = charToNum(ch);
            int p = (c - key - (i * i) + 26) % 26;
            plaintext[i] = numToChar(p, ch);
        } else {
            plaintext[i] = ch;
        }
    }
    plaintext[i] = '\0';
}

int main() {
    char plaintext[100], ciphertext[100], recovered[100];
    int key;

    printf("Enter plaintext (a-z, A-Z allowed): ");
    scanf("%s", plaintext);
    printf("Enter key (0-25): ");
    scanf("%d", &key);

    encrypt(plaintext, ciphertext, key);
    printf("Encrypted text: %s\n", ciphertext);

    decrypt(ciphertext, recovered, key);
    printf("Decrypted text: %s\n", recovered);

    return 0;
}
```

---

## 📂 Project Structure
```
alpha-matrix-cipher/
├── alpha_matrix_cipher.c
├── README.md
├── test_case.txt
└── flowchart.png   ← optional
```

---

## ✅ Key Features:
- Works with both **lowercase and uppercase** letters.
- Ignores and preserves **non-letter characters**.
- Uses **modular arithmetic (mod 26)** for cyclic transformation.
- More secure and position-sensitive than simple Caesar ciphers.

---

## ✅ Example:

- **Plaintext:** `hello`  
- **Key:** `3`

### Step-by-step:

| i | P[i] | i² | Calculation | C[i] | Letter |
|---|------|----|-------------|------|--------|
| 0 | 7    | 0  | (7+3+0)%26  | 10   | k      |
| 1 | 4    | 1  | (4+3+1)%26  | 8    | i      |
| 2 | 11   | 4  | (11+3+4)%26 | 18   | s      |
| 3 | 11   | 9  | (11+3+9)%26 | 23   | x      |
| 4 | 14   | 16 | (14+3+16)%26| 7    | h      |

**Encrypted:** `kisxh`  
**Decrypted:** `hello`

---

> 🔐 *AlphaMatrix Cipher - Secure, Structured, and Simple.*  
> Happy Encrypting!
