[简体中文](README.md) | English
# Merkle Tree Implementation

A high-performance Merkle Tree implementation in MoonBit, supporting tree creation, proof generation, and verification. Suitable for data integrity verification and blockchain applications.

## 🌟 Core Features

• 🔐 **Hash Function Encapsulation** – Customizable hash functions, default is keccak256  
• 📊 **Input Data Handling** – Accepts arrays of any type, supports strings, integers, etc.  
• 🍃 **Leaf Node Generation** – Hashes each data item to form leaf nodes  
• 🌲 **Recursive Parent Node Construction** – Automatically builds the full tree from leaves  
• 📜 **Proof Generation** – Generates proof paths for single or multiple leaves  
• ✅ **Proof Verification** – Verifies the validity of single or multiple proofs  
• 🔄 **Odd Node Support** – Automatically handles odd number of nodes  
• 🛠️ **Custom Hash** – Supports custom leaf and node hash functions

## 📥 Installation & Setup

```bash
# Clone the repository
git clone https://github.com/0Ayachi0/MerkleTree.git

# Enter the project directory
cd MerkleTree

# Build the project
moonc build

# Run tests
moonc test
```

## 🚀 Usage Guide

### 🔨 Create a Merkle Tree

Quickly create a string or integer Merkle tree with predefined functions:

```moonbit
// Create a string Merkle tree
let values = ["apple", "banana", "cherry", "date"]
let tree = create_string_tree(values)

// Create an integer Merkle tree
let numbers = [1, 2, 3, 4, 5]
let int_tree = create_int_tree(numbers)

// Check tree size
assert_eq!(length(tree), 4)
assert_eq!(length(int_tree), 5)
```

### 🔍 Verify Elements

Verify if an element is in the tree and if the proof is valid:

```moonbit
// Get the index of an element
let index = get_value_index(tree, "cherry")
assert_eq!(index, 2)  // "cherry" is at index 2

// Verify element existence (in practice, proof should be obtained from the tree)
let proof = [] // Simplified example, use actual proof in real use
let is_valid = verify_string_in_tree(tree, "apple", proof)
```

### 📜 Multi-Proof

Verify multiple elements at once:

```moonbit
// Create a multi-proof
let multi_proof = MultiProof::{
  leaves: ["apple", "cherry"],
  proof: [], // Should be generated from the tree
  proof_flags: [true] // Should be generated from the tree
}

// Verify multi-proof
let is_multi_valid = verify_multi(tree, multi_proof)
```

### 🛠️ Custom Hash Functions

Create a Merkle tree with a custom hash function:

```moonbit
// Custom leaf hash function
let custom_leaf_hash = fn(s : String) -> HexString {
  // Custom hash logic
  keccak256(abi_encode(["string", "uint256"], [s, "1"], fn(s : String) -> String { s }))
}

// Create tree with custom hash
let custom_tree = create_tree(values, custom_leaf_hash)
```

### 🔄 Get Tree Root Hash

Get the Merkle tree root hash for integrity verification:

```moonbit
// Get root hash
let root_hash = root(tree)
println("Merkle tree root hash: " + root_hash)

// Verify element with root hash
let is_valid = verify_with_root(
  "apple", 
  proof, 
  root_hash, 
  hash_string
)
```

### 📊 Basic Tree Operations

Check basic properties and operations:

```moonbit
// Check if tree is empty
let is_empty = is_empty(tree)
assert_false!(is_empty)

// Get value at specific index
let value = value_at(tree, 0)
assert_eq!(value, "apple")

// Get string representation of the tree
let tree_str = to_string(tree, fn(s) { "\"" + s + "\"" })
println(tree_str)
```

## 📋 Full API Reference

### Core Functions
- `create_tree(values, leaf_hash, node_hash)` - Create a Merkle tree
- `root(tree)` - Get the root hash
- `length(tree)` - Get the size of the tree
- `is_empty(tree)` - Check if the tree is empty
- `value_at(tree, index)` - Get the value at a specific index

### Proof Related
- `verify(tree, value, proof)` - Verify a single proof
- `verify_with_root(value, proof, root, leaf_hash)` - Verify proof with root hash
- `verify_multi(tree, multi_proof)` - Verify multi-proof
- `verify_multi_with_root(multi_proof, root, leaf_hash)` - Verify multi-proof with root hash

### Helper Functions
- `create_string_tree(values)` - Create a string Merkle tree
- `create_int_tree(values)` - Create an integer Merkle tree
- `hash_string(s)` - String hash function
- `hash_int(n)` - Integer hash function
- `to_string(tree, value_to_string)` - Get string representation of the tree

## 📊 Performance

| Operation         | Time Complexity | Space Complexity |
|------------------|----------------|-----------------|
| Create tree      | O(n log n)     | O(n)            |
| Get root hash    | O(1)           | O(1)            |
| Verify proof     | O(log n)       | O(log n)        |
| Verify multi     | O(m log n)     | O(m + log n)    |

Where n is the number of elements, m is the number of elements in the multi-proof.

## 🏗️ Implementation Details

This Merkle tree implementation is based on the following core components:

- **Leaf Hash Function**: Converts input data to fixed-length hash
- **Node Hash Function**: Combines and hashes two child nodes
- **Tree Structure**: Stores all nodes in an array for fast access
- **Proof Generation**: Generates path from leaf to root for each leaf
- **Proof Verification**: Recomputes hashes to verify proof validity

### Advanced Features
- **Type Safety**: Generic support for any hashable type
- **Custom Hash**: Supports custom hash functions
- **Multi-Proof**: Supports verifying multiple elements at once
- **Odd Node Handling**: Automatically handles odd number of nodes

## 🔍 Example Files

The project includes two main example files:

- `simple.mbt`: Shows basic Merkle tree operations
- `standard.mbt`: Shows standard Merkle tree operations

## 🧪 Testing

The project includes several test files to ensure correctness:

- `bytes_test.mbt`: Byte handling tests
- `hashes_test.mbt`: Hash function tests
- `MerkleTree_test.mbt`: Merkle tree functionality tests

Run tests:

```bash
moonc test
```

## 📚 Use Cases

- **Blockchain**: Verify if a transaction is included in a block
- **Distributed Databases**: Data integrity verification
- **P2P Networks**: Efficient data consistency checks
- **Content Addressed Storage**: Content integrity verification
- **Zero-Knowledge Proofs**: As a component in ZKP systems

## 📜 License

This project is licensed under the Apache-2.0 License. See LICENSE for details.

## 📢 Contact & Support

• MoonBit Community: moonbit-community  
• GitHub Issues: [Report Issues](https://github.com/0Ayachi0/MerkleTree/issues)

👋 If you like this project, please give it a ⭐! Happy coding! 🚀
