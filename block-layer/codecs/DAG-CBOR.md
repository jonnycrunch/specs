# Specification: DAG-CBOR

**Status: Descriptive - Final**

DAG-CBOR supports the full [IPLD Data Model](../data-model-layer/data-model.md).

CBOR already natively supports all [IPLD Data Model Kinds](../data-model-layer/data-model.md#kinds).

## Format

The CBOR IPLD format is called DagCBOR to disambiguate it from regular CBOR.
Most CBOR objects are valid DagCBOR. The only hard restriction is that any field
with the tag 42 must be a valid CID.

## Link Format

As with all IPLD formats, DagCBOR must be able to encode merkle-links. In
DagCBOR, links are encoded using the raw-binary (identity, NUL) multibase in a
field with a byte-string type (major type 2), with the tag 42.

(the inclusion of the multibase exists for historical reasons)

## Map Key Restriction

In DagCBOR, map keys must be strings (TODO: drop this? We already have
unpathable map keys). Furthermore, map keys should avoid using `/` as this is
unpathable (TODO: drop this? IMO, we should support path escaping out of the
box).

## Canonical DagCBOR

Canonical DagCBOR must:

1. Use no tags other than the CID tag (42). Other tags may be lost in
   conversion.
2. Use the [canonical CBOR](https://tools.ietf.org/html/rfc7049#section-3.9)
   encoding.
3. Only use string map keys. Some implementations may not be able to
   handle non-string keys.
