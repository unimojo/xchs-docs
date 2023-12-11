# Protocol

- The inscription of XCHS is inscribed in the transfer Memo of regular XCH.
- The supported XCH transfer type is the standard XCH transfer type: `p2_delegated_puzzle_or_hidden_puzzle`
- Due to the limitations of Chialisp, there are slight differences compared to standard JSON: content must use single quotes `'`, and it is not allowed to have single or double quotes (`'`, `"`) within the content.
- The content of XCHS in the Memo includes two parts:
  - Hint: A 256-bit hash, calculated as: `SHA256("{'p':'xchs','tick':'paws'}")`
  - Inscription: The content of the inscription. Please note to not include spaces, such as: `{'p':'xchs','op':'mint','tick':'paws','amt':'1000'}`