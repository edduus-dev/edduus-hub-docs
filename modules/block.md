This is sub-document of Edduus Hub documentation. For the reference, please refer to the [parent document](README.md).

# Block Module

## Overview

Analogous to blocks in blockchain, “blocks” in the Edduus education system are best described as individual components of all learning activities. Blocks are too often seen as discrete elements of curriculum that can be assembled differently for each individual to provide deeper understanding in the context of the individual’s current learning juncture.

Blocks are generally available to the public, with the only exception being exclusive blocks where only explicitly designated learners have access. A block defines what can be learned in that block, and shall not be confused with the actual learning material nor the resources used to provide them. Blocks can be uniquely identified by their titles, and are classified by language and level of education. Blocks are generally concluded by an assessment at the end of each block, the criteria of which must be specified in the corresponding block. Each Block also incorporates assessments which may include a responsive online test specifically for the Block. In addition to a responsive online test, a Block assessment may be specified by its criteria/rubric enabling teacher and/or self assessment. Block assessment data is maintained indelibly on the blockchain, and the assessment process incorporates features including:

- Encrypted communication
- Identity masking
- Proctoring
- Remote control
- Biometric signature
- Facial recognition

#### Note: This module is in active development, and actual commands may vary.

## Create a new block

Using CLI

```bash
edcli tx edblock create "Building Your Own Programming Language" "Learn language building techniques: Lexing, Parsing, Tokenization, and Traversing Abstract Syntax Trees." --from teacher
```

## Query specific block by ID (SHA256 signature)

```bash
edcli q edblock get 67630ab66ba4c49e84820b4eefbf9e73f087d15856035090051fa227bbf0af1e
# Output:
{
  "title": "Building Your Own Programming Language",
  "description": "Learn language building techniques: Lexing, Parsing, Tokenization, and Traversing Abstract Syntax Trees."
}
```

## Query all blocks

```bash
edcli q edblock all
```
