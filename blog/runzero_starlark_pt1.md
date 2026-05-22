# Building a Custom Integration in runZero with Starlark (Part 1)

In this blog series we'll be examining the steps and workflows I use for creating a custom integration in runZero. Our test subject will be a custom integration to Wazuh but the general workflow is applicable to most custom integration scripts.

## What is Starlark

Starlark was originally designed by Google as a programmatic configuration language for Bazel (also created by Google), an open-source tool for automated building and testing of software. Originally known as Skylark, Starlark provides a means of defining build rules and macros for Bazel. For many, Starlark will have familiar syntax as it is a dialect of Python, though it uses only a subset of Python syntax.




Starlark (formerly known as Skylark) is a deterministic, high-level configuration language designed by Google. It is a subset of Python, specifically tailored to be embedded in larger applications to provide safe, hermetic, and parallelizable scripting capabilities. 
While it is most famous as the extension language for the Bazel build system, it has been adopted by numerous other tools like Buck2, Tilt, and Drone CI. 
Key Characteristics
Starlark is designed to solve the "messy" problems of using a general-purpose language like Python for critical tasks like build configurations. Its design focuses on:
Determinism: Executing the same code twice with the same inputs will always yield the exact same result.
Hermeticity: By default, Starlark cannot access the file system, network, or system clock. This ensures that scripts are portable and don't have "hidden" dependencies.
Parallel Execution: Because shared data structures are "frozen" (made immutable) after evaluation, multiple Starlark threads can run in parallel without risk of data races.
Simplicity: It removes complex Python features such as classes, exceptions, reflection, and recursion to maintain a low learning curve and predictable performance. 
Key Syntax & Language Features
Starlark's syntax is a strict subset of Python, meaning most Starlark code is also valid Python code. 
Supported Types: Includes None, bool, dict, list, int, string, tuple, and function.
Mutability: Lists and dictionaries are mutable during their initial creation but are "frozen" and become immutable once the module finished loading.
No Recursion: To prevent infinite loops and stack overflows, Starlark explicitly forbids recursive function calls.
Load Statement: Instead of import, Starlark uses the load() function to import symbols from other modules. 
Popular Implementations
There are three primary production-ready implementations of the Starlark interpreter: 
Java (Bazel): The original implementation used within the Bazel build system.
Go (starlark-go): A popular implementation for embedding Starlark in Go-based tools.
Rust (starlark-rust): Developed by Meta for the Buck2 build system, known for its performance and modern features. 
Common Use Cases
Build Systems: Defining build rules and logic in Bazel and Buck2.
CI/CD Pipelines: Scripting complex pipelines in Drone or Vela.
Configuration Management: Managing Kubernetes configurations with Tilt or ytt.
Workflow Automation: Defining logic in platforms like AutoKitteh or Copybara. 



## When is Starlark appropriate for a custom integration?

Starlark is a perfect choice for a ReSTful or Graph API that can be interacted with using HTTP reques methods and that also returns responses formatted in JSON. 

## Starlark modules




## Creating Credentials and Authenticating to the API endpoint(s)

The first step in building any integration is successfully authenticating to the API. There are a number of different authentication methods and we will take a look at the most common ones I've come across. runZero's implementation of starlark also support two different modules for making HTTP requests so examples will be shown for both.

### Basic Auth

### Bearer Token

### Client ID and Client Secret (Oauth 2.0)

