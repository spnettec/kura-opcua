# Retained OPC UA driver regression tests

The official upstream snapshot `aee29e9f` uses Milo 0.6.16; this fork deliberately uses Milo 1.1.2. These versions differ in artifact names, encoding context and asynchronous client APIs. The restored basic tests exercise the current driver, without downgrading or changing production dependencies.

Nine JUnit 5 test methods pass under Maven 3.10/JDK 21. Client mocks use `getStaticEncodingContext()` and `readAsync()`, with completed futures. The datatype test checks byte-array contents as well as the declared Kura datatype. Descriptor checks distinguish stable IDs from the fork's `%...` localized names. They include successful and invalid reads, missing nodes and prepared reads; no external OPC UA endpoint is contacted.

```sh
mvn test
```

YOFC uses its independent PLC4J OPC UA integration. This repository retains the existing official driver. The historical Milo 0.6.16 test-server/OSGi harness is not treated as compatible with 1.1.2 or as a passed integration suite; that distinction is recorded in the workspace inventory. No server-side feature expansion is part of this restoration.
