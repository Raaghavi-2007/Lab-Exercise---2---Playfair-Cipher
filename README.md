# Lab-Exercise---2---Playfair-Cipher

# Aim:
  To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.
  
# Procedure:

Step 1: 
Design of PlayFair Cipher algorithm to encrypt plaintext using a key and a 5 × 5 key matrix..

Step 2:
Implementation using C or python code.

Step 3:
Testing algorithm with different key values and plaintext inputs.

Step 4:
Apply Playfair Cipher using with different key and verify the corresponding encrypted outputs.

Step 5:
Observe and record the encrypted text for each test case.

# Program:
```
def generate_matrix(key):
    key = key.upper().replace("J", "I")
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    text = ""

    for ch in key + alphabet:
        if ch.isalpha() and ch not in text:
            text += ch

    return [list(text[i:i+5]) for i in range(0, 25, 5)]


def prepare_text(text):
    text = text.upper().replace("J", "I")
    text = "".join(ch for ch in text if ch.isalpha())
    pairs = []
    i = 0

    while i < len(text):
        a = text[i]

        if i + 1 == len(text):
            b = 'X'
            i += 1
        elif text[i] == text[i + 1]:
            b = 'X'
            i += 1
        else:
            b = text[i + 1]
            i += 2

        pairs.append(a + b)

    return pairs


def playfair_encrypt(plaintext, key):
    matrix = generate_matrix(key)
    pairs = prepare_text(plaintext)
    ciphertext = ""

    def position(ch):
        for r in range(5):
            for c in range(5):
                if matrix[r][c] == ch:
                    return r, c

    for pair in pairs:
        r1, c1 = position(pair[0])
        r2, c2 = position(pair[1])

        if r1 == r2:
            ciphertext += matrix[r1][(c1 + 1) % 5]
            ciphertext += matrix[r2][(c2 + 1) % 5]

        elif c1 == c2:
            ciphertext += matrix[(r1 + 1) % 5][c1]
            ciphertext += matrix[(r2 + 1) % 5][c2]

        else:
            ciphertext += matrix[r1][c2]
            ciphertext += matrix[r2][c1]

    return matrix, pairs, ciphertext


key = input("Enter the key: ")
plaintext = input("Enter the plaintext: ")

matrix, pairs, encrypted = playfair_encrypt(plaintext, key)

print("\nKey Matrix:")
for row in matrix:
    print("".join(row))

print("\nPlaintext pairs:", " ".join(pairs))
print("Encrypted text:", encrypted)

```

# Output:

<img width="1917" height="562" alt="image" src="https://github.com/user-attachments/assets/9008efc3-54a2-4bce-b39c-f39481cff313" />

# Result:
The program is executed successfully.
