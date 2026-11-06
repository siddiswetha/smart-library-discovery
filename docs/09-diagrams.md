# Diagrams — Smart Library Discovery

These are simple diagrams to help a beginner see how the product works. They match the spec in `docs/03-spec.md`. No image files are used — the diagrams below are written in Mermaid text, which GitHub renders as a picture.

## 1. How it works

```mermaid
flowchart TD
    A["Student types a topic or a partial title"] --> B["Understand the query, including misspellings"]
    B --> C["Search the library catalogue only"]
    C --> D["Show exact matches with location and availability"]
    D --> E["Show close alternatives separately, with the reason why"]
    E --> F{"No match in the catalogue?"}
    F -- Yes --> G["Say it is not in the catalogue, and show the nearest alternative"]
    F -- No --> H["Student finds a usable book"]
```

What this shows: the system never invents availability or a shelf location. Exact matches and alternatives are kept clearly separate, so the student is not misled.

## 2. User journey

```mermaid
flowchart TD
    A["Student needs a book for an assignment"] --> B["Student searches by topic, not by exact title"]
    B --> C["Student finds the exact book in the top 3 results"]
    C --> D["Student checks the edition and availability"]
    D --> E["Student goes to the shelf"]
    E --> F["Student uses a real source instead of buying the book"]
```

What this shows: before the product, a failed search meant the student thought the library did not have the book. After it, the student finds the book and can trust the availability shown.

## 3. Eval and release flow

```mermaid
flowchart TD
    A["Build the 40-search test set"] --> B["Run the searches"]
    B --> C{"Is availability 100 percent right, and top-3 discovery at least 85 percent?"}
    C -- No --> D["Fix the search or the routing"]
    D --> B
    C -- Yes --> E["Librarian reviews the eval before any student sees it"]
    E --> F["Help-desk pilot for 2 weeks, logging every wrong result"]
    F --> G["Expand to student self-service"]
```

What this shows: a librarian checks the product before students do, and the help-desk pilot proves it in real use before it is opened to everyone.
