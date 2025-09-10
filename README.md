
````markdown
# HashTable with Linear Probing in Python

A simple hash table implementation using **open addressing** with **linear probing** for collision resolution. This hash table supports insertion, searching, and deletion of integer keys.

---

## Features

- Fixed-size hash table
- Hash function using the division method (`key % size`)
- Collision handling with linear probing
- Deletion handled using `"DELETED"` markers to maintain probe sequences
- Console display of the hash table contents

---

## Code Overview

```python
class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size

    # Hash function (division method)
    def hash_function(self, key):
        return key % self.size

    # Insert a key
    def insert(self, key):
        index = self.hash_function(key)
        start_index = index

        while self.table[index] is not None and self.table[index] != "DELETED":
            index = (index + 1) % self.size
            if index == start_index:  # Table is full
                print("Hash table is full. Cannot insert", key)
                return
        self.table[index] = key

    # Search for a key
    def search(self, key):
        index = self.hash_function(key)
        start_index = index

        while self.table[index] is not None:
            if self.table[index] == key:
                return index
            index = (index + 1) % self.size
            if index == start_index:  # Looped back
                break
        return -1

    # Delete a key
    def delete(self, key):
        index = self.search(key)
        if index == -1:
            print(key, "not found.")
        else:
            self.table[index] = "DELETED"
            print(key, "deleted.")

    # Display the table
    def display(self):
        for i in range(self.size):
            print(i, ":", self.table[i])


# ---------------- Example Usage ----------------
ht = HashTable(7)   # hash table of size 7

ht.insert(10)
ht.insert(25)
ht.insert(15)
ht.insert(7)
ht.insert(90)

print("\nHash Table after insertions:")
ht.display()

print("\nSearching 15:", "Found at index" if ht.search(15) != -1 else "Not Found")
print("Searching 99:", "Found at index" if ht.search(99) != -1 else "Not Found")

ht.delete(25)

print("\nHash Table after deleting 20:")  # Note: the key deleted was 25, update this line as needed.
ht.display()
````

---

## How It Works

* The hash function calculates the index by `key % size`.
* On collision, linear probing searches the next available slot sequentially.
* Deleted keys are marked as `"DELETED"` so probing during search and insertion works correctly.
* Searching stops if the key is found or when it loops back to the start index.

---

## Limitations

* Only supports integer keys.
* Fixed size with no resizing mechanism.
* The table can become inefficient with many `"DELETED"` slots over time.

---

## Suggestions for Improvement

* Add dynamic resizing and rehashing to maintain performance.
* Extend support to other key types (e.g., strings).
* Explore other collision resolution methods like quadratic probing or chaining.


````

---

**Note:**  
You might want to fix the print message after deletion since you delete `25` but print `deleting 20`. Just change:

```python
print("\nHash Table after deleting 20:")
````

to

```python
print("\nHash Table after deleting 25:")
```
