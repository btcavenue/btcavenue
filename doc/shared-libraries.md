Shared Libraries
================

## btcavenueconsensus

The purpose of this library is to make the verification functionality that is critical to Btcavenue's consensus available to other applications, e.g. to language bindings.

### API

The interface is defined in the C header `btcavenueconsensus.h` located in `src/script/btcavenueconsensus.h`.

#### Version

`btcavenueconsensus_version` returns an `unsigned int` with the API version *(currently `1`)*.

#### Script Validation

`btcavenueconsensus_verify_script` returns an `int` with the status of the verification. It will be `1` if the input script correctly spends the previous output `scriptPubKey`.

##### Parameters
- `const unsigned char *scriptPubKey` - The previous output script that encumbers spending.
- `unsigned int scriptPubKeyLen` - The number of bytes for the `scriptPubKey`.
- `const unsigned char *txTo` - The transaction with the input that is spending the previous output.
- `unsigned int txToLen` - The number of bytes for the `txTo`.
- `unsigned int nIn` - The index of the input in `txTo` that spends the `scriptPubKey`.
- `unsigned int flags` - The script validation flags *(see below)*.
- `btcavenueconsensus_error* err` - Will have the error/success code for the operation *(see below)*.

##### Script Flags
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_NONE`
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_P2SH` - Evaluate P2SH ([BIP16](https://github.com/btcavenue/bips/blob/master/bip-0016.mediawiki)) subscripts
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_DERSIG` - Enforce strict DER ([BIP66](https://github.com/btcavenue/bips/blob/master/bip-0066.mediawiki)) compliance
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_NULLDUMMY` - Enforce NULLDUMMY ([BIP147](https://github.com/btcavenue/bips/blob/master/bip-0147.mediawiki))
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_CHECKLOCKTIMEVERIFY` - Enable CHECKLOCKTIMEVERIFY ([BIP65](https://github.com/btcavenue/bips/blob/master/bip-0065.mediawiki))
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_CHECKSEQUENCEVERIFY` - Enable CHECKSEQUENCEVERIFY ([BIP112](https://github.com/btcavenue/bips/blob/master/bip-0112.mediawiki))
- `btcavenueconsensus_SCRIPT_FLAGS_VERIFY_WITNESS` - Enable WITNESS ([BIP141](https://github.com/btcavenue/bips/blob/master/bip-0141.mediawiki))

##### Errors
- `btcavenueconsensus_ERR_OK` - No errors with input parameters *(see the return value of `btcavenueconsensus_verify_script` for the verification status)*
- `btcavenueconsensus_ERR_TX_INDEX` - An invalid index for `txTo`
- `btcavenueconsensus_ERR_TX_SIZE_MISMATCH` - `txToLen` did not match with the size of `txTo`
- `btcavenueconsensus_ERR_DESERIALIZE` - An error deserializing `txTo`
- `btcavenueconsensus_ERR_AMOUNT_REQUIRED` - Input amount is required if WITNESS is used

### Example Implementations
- [NBtcavenue](https://github.com/NicolasDorier/NBtcavenue/blob/master/NBtcavenue/Script.cs#L814) (.NET Bindings)
- [node-libbtcavenueconsensus](https://github.com/bitpay/node-libbtcavenueconsensus) (Node.js Bindings)
- [java-libbtcavenueconsensus](https://github.com/dexX7/java-libbtcavenueconsensus) (Java Bindings)
- [btcavenueconsensus-php](https://github.com/Bit-Wasp/btcavenueconsensus-php) (PHP Bindings)
