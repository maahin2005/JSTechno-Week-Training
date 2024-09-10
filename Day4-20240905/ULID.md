# ULID

## ULID (Universally Unique Lexicographically Sortable Identifier)

### ULID is a 128-bit identifier, but its string representation is more compact and lexicographically sortable.
- Example: 01ARZ3NDEKTSV4RRFFQ69G5FAV

- Structure:
    - Timestamp Component: The first 48 bits encode the millisecond-precision timestamp.
    - Random Component: The remaining 80 bits are randomly generated.

- Properties:

    - Chronological Ordering: ULIDs are lexicographically sortable, meaning that newer identifiers are guaranteed to come after older ones, which makes them better suited for ordered datasets.
    - Uniqueness: ULIDs ensure uniqueness like UUIDs but are optimized for sorting by timestamp.
    - Human-Readable: ULIDs are more compact than UUIDs and can be easier to work with in URLs or for debugging purposes.

- Use Case:

    - Useful when you need globally unique IDs that can also be sorted by creation time, such as in logs, time-series databases, or event stores.
    - Good for systems where ordering matters and efficient querying by date/time is important.