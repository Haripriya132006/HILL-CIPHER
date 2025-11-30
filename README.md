# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
import math

# Convert letter → number (A=0,...Z=25)
def text_to_nums(text):
    return [ord(c) - 65 for c in text.upper() if c.isalpha()]

# Convert number → letter
def nums_to_text(nums):
    return ''.join(chr(n + 65) for n in nums)

# Break text into chunks of size n
def chunkify(nums, n):
    while len(nums) % n != 0:
        nums.append(0)  # padding with 'A'
    return [nums[i:i+n] for i in range(0, len(nums), n)]

# Multiply matrix × vector (mod 26)
def mat_mul(M, vec):
    return [(M[0][0]*vec[0] + M[0][1]*vec[1]) % 26,
            (M[1][0]*vec[0] + M[1][1]*vec[1]) % 26]

# Compute inverse of 2×2 matrix mod 26
def inverse_matrix(M):
    det = (M[0][0]*M[1][1] - M[0][1]*M[1][0]) % 26
    if math.gcd(det, 26) != 1:
        raise ValueError("Key is NOT invertible modulo 26.")

    det_inv = pow(det, -1, 26)  # modular inverse

    return [
        [( M[1][1] * det_inv) % 26, (-M[0][1] * det_inv) % 26],
        [(-M[1][0] * det_inv) % 26, ( M[0][0] * det_inv) % 26]
    ]

# Encrypt
def encrypt(pt, key):
    nums = text_to_nums(pt)
    chunks = chunkify(nums, 2)

    result = []
    for c in chunks:
        result.extend(mat_mul(key, c))
    return nums_to_text(result)

# Decrypt
def decrypt(ct, key):
    key_inv = inverse_matrix(key)

    nums = text_to_nums(ct)
    chunks = chunkify(nums, 2)

    result = []
    for c in chunks:
        result.extend(mat_mul(key_inv, c))
    return nums_to_text(result)


# ----------- MAIN PROGRAM -------------

print("Hill Cipher (2×2 key only)\n")

k = input("Enter 4-letter key (example: HILL): ").upper()
if len(k) != 4 or not k.isalpha():
    print("Invalid key!")
    exit()

# Build 2×2 key matrix
key = [
    [ord(k[0]) - 65, ord(k[1]) - 65],
    [ord(k[2]) - 65, ord(k[3]) - 65]
]

mode = input("Encrypt or Decrypt? (E/D): ").upper()

if mode == "E":
    pt = input("Enter plaintext: ")
    print("Ciphertext:", encrypt(pt, key))

elif mode == "D":
    ct = input("Enter ciphertext: ")
    print("Plaintext:", decrypt(ct, key))

else:
    print("Invalid option!")

```
## OUTPUT
<img width="1595" height="598" alt="image" src="https://github.com/user-attachments/assets/86312302-e09a-4b0c-9532-ad038bfe1d3e" />

<img width="1595" height="598" alt="image" src="https://github.com/user-attachments/assets/78bd437a-9628-44cd-a55c-2d6a01b33d4a" />

## RESULT
