# UUID

## UUID (Universally Unique Identifier)

### UUID is a 128-bit number, often represented as a 36-character string.

- Example: 550e8400-e29b-41d4-a716-446655440000

- Versions:

    - There are different versions of UUIDs. The most common are:
    - UUIDv1: Generated using a combination of the current timestamp and the machine's MAC address.
    - UUIDv4: Randomly generated.
    - UUIDv5: Generated using a namespace and a name (hash-based).

- Properties:

    - Global Uniqueness: Ensures uniqueness across systems, though collisions are possible in theory, they are highly unlikely.
    - Non-Sequential: UUIDs (particularly UUIDv4) are not ordered chronologically and can’t be easily sorted by generation time.
    - Length: UUIDs are relatively long, which can have performance implications for indexing in databases.

- Use Case:

    - Good for generating unique keys in distributed systems where uniqueness is crucial.
    - Commonly used as primary keys in databases where uniqueness is required but order doesn't matter.