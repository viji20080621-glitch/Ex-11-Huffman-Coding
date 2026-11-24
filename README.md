# IMPLEMENTATION OF HUFFMAN CODING
# Aim
To implement Huffman coding to compress the data using Python programming.

# Software Required
1. Anaconda – Python 3.7
2. Jupyter Notebook

# Algorithm

- Step 1: Get the input string from the user.

- Step 2: Calculate the frequency of occurrence of each character in the input string.

- Step 3: Create leaf nodes for each character and construct a Huffman tree by repeatedly combining the two nodes with the lowest frequencies.

- Step 4: Generate Huffman codes by assigning 0 to the left branch and 1 to the right branch.

- Step 5: Display each character along with its corresponding Huffman code.

# Program
# Developed By
# Name: Vijiyalakshmi A
# Register No: 212225240185

```p

import heapq
from collections import Counter

class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq

def build_huffman_tree(text):
    frequency = Counter(text)
    heap = [Node(char, freq) for char, freq in frequency.items()]
    heapq.heapify(heap)

    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)

        merged = Node(None, left.freq + right.freq)
        merged.left = left
        merged.right = right

        heapq.heappush(heap, merged)

    return heap[0]

def generate_codes(root, code="", codes=None):
    if codes is None:
        codes = {}

    if root.char is not None:
        codes[root.char] = code if code else "0"
        return codes

    generate_codes(root.left, code + "0", codes)
    generate_codes(root.right, code + "1", codes)

    return codes

def huffman_compress(text):
    root = build_huffman_tree(text)
    codes = generate_codes(root)

    compressed = ''.join(codes[char] for char in text)

    return codes, compressed

text = input("Enter the text: ")

if text:
    codes, compressed = huffman_compress(text)

    print("\nCharacter Frequencies:")
    for char, freq in Counter(text).items():
        print(repr(char), ":", freq)

    print("\nHuffman Codes:")
    for char, code in codes.items():
        print(repr(char), ":", code)

    print("\nOriginal Text:", text)
    print("Compressed Binary:", compressed)
    print("Original Size:", len(text) * 8, "bits")
    print("Compressed Size:", len(compressed), "bits")

    ratio = (1 - len(compressed) / (len(text) * 8)) * 100
    print("Compression Percentage:", round(ratio, 2), "%")
else:
    print("Please enter some text.")

```

# Output

<img width="765" height="717" alt="image" src="https://github.com/user-attachments/assets/0fa0a30b-5bbd-4ea7-ba1b-3f9382ccfcd8" />

# Result

Thus, Huffman coding was successfully implemented to compress the data using Python programming.
