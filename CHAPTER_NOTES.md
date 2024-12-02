# Notes from Effective React with NX

## Chapter 2

### The directions in the book differ enough from the current state of Nx tooling, that the book should not be used. For instance, the `appDirectory` option was responsible for tying the library into the bookstore app. I will prefer to look for an updated solution that connects generated code consistently.
- 80% of the logic should reside in libraries, 20% in apps.
- Ease of re-use might emerge as a positive side-effect of refactoring code into libraries by applying an “API thinking” approach. It is not the main driver though.
- Example file structure for specifiying UI to the "books" domain, or general purpose UI components. Also useful for applying code ownership rules & boundaries.
```bash
.
├── (...)
├── libs
│ └── books
│ │ └── feature
│ │ │ ├── src
│ │ │ ├── ...
│ │ │ └── ...
│ │ └── ui
│ │ ├── src
│ │ ├── ...
│ │ └── ...
│ └── ui
│ ├── src
│ ├── ...
│ └──
```
- In a workspace, libraries are typically divided into four different types:
    - Feature: Libraries that implement “smart” UI (e.g. is effectful, is connected to data sources, handles routing, etc.) for specific business use cases.
    - UI: Libraries that contain only presentational components. That is, components that render purely from their props, and calls function handlers when interaction occurs.
    - Data-access: Libraries that contain the means for interacting with external data services; external services are typically backend services.
    - Utility: Libraries that contain common utilities that are shared by many projects.
- We can form rules about what each types of libraries can depend on. For example, UI libraries cannot use feature or data-access libraries, because doing so will mean that they are effectful. This demarcation makes it easier to understand the capabilities of each library, and how they interact with each other.
- to create feature library (just choose defaults):
```bash
# note: type:feature tag may not exist anymore
npx nx generate @nx/js:lib libs/books/feature \ 
--tags scope:books
```