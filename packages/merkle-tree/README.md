# @ergoplatform/merkle-tree [![npm](https://badgen.net/npm/v/@ergoplatform/merkle-tree)](https://www.npmjs.com/package/@ergoplatform/merkle-tree) 

This package provides functionality for working with merkle trees.

Merkle trees are commonly used in distributed systems and blockchain applications to verify the integrity of data that is stored or transmitted across multiple nodes.

## Installation

For nodejs and bundler based frontend projects this package can be installed via NPM:

```sh
npm install @ergoplatform/merkle-tree
```

It can also be used in pure browser based code like so:

```html
<body>
    <script type="module" src="https://cdn.jsdelivr.net/npm/@ergoplatform/merkle-tree@latest/dist/browser/ergo_merkle_tree_wasm.min.js"></script>

    <script type="module">
        import init, {LevelNode, MerkleProof} from 'https://cdn.jsdelivr.net/npm/@ergoplatform/merkle-tree@latest/dist/browser/ergo_merkle_tree_wasm.min.js';

        function hexToBytes(hexStr) {
            return Uint8Array.from(
                hexStr.match(/.{1,2}/g).map((byte) => parseInt(byte, 16))
            );
        }

        await init('https://cdn.jsdelivr.net/npm/@ergoplatform/merkle-tree@latest/dist/browser/ergo_merkle_tree_wasm_bg.wasm');

        const levels = hexToBytes("0139b79af823a92aa72ced2c6d9e7f7f4687de5b5af7fab0ad205d3e54bda3f3ae");
        const levelNode = new LevelNode(levels.slice(1), levels[0]);

        const preImage = hexToBytes(
            "01fb9e35f8a73c128b73e8fde5c108228060d68f11a69359ee0fb9bfd84e7ecde6d19957ccbbe75b075b3baf1cac6126b6e80b5770258f4cec29fbde92337faeec74c851610658a40f5ae74aa3a4babd5751bd827a6ccc1fe069468ef487cb90a8c452f6f90ab0b6c818f19b5d17befd85de199d533893a359eb25e7804c8b5d7514d784c8e0e52dabae6e89a9d6ed9c84388b228e7cdee09462488c636a87931d656eb8b40f82a507008ccacbee05000000"
        );
        const txRoot = preImage.slice(65, 97);
        const txId = hexToBytes(
            "642c15c62553edd8fd9af9a6f754f3c7a6c03faacd0c9b9d5b7d11052c6c6fe8"
        );

        const proof = new MerkleProof(txId, [levelNode]);

        console.log('tx proof is valid: ', proof.isValid(txRoot));
    </script>
</body>
```
