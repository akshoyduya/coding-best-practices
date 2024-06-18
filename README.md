I have prepared this document explaining all the coding best practices and the process that one can follow.
I have also mentioned the best practices for writing clean code. This will also help in maintaining the code quality and
consistency across the codebase.

We can grow the list as we go along and learn and follow new best practices.

### Coding Process Best Practices

1. **Naming Conventions**
    - Use meaningful names for variables, functions, classes, etc.
    - Use camelCase for variables and functions.
    - Use PascalCase for classes.
    - Use UPPERCASE for constants.
    - Use snake_case for file names.
    - Use a consistent naming convention throughout the codebase.

2. **Code Formatting**
    - Use Es/Ts linting rules to format the code.

3. **Comments**
    - Class, Function, and Variable should be self-explanatory.
    - Use comments to explain complex code. If you need to explain the architecture of the code, drop a link to the
      architecture document or a JIRA ticket.

4. **Code Structure**
    - Use a consistent code, folder, file structure, throughout the codebase.

5. **Error Handling**
    - If the error is expected, log it as a warning or info. but if it's unexpected, log it as an error. Otherwise, we
      will keep getting false positives in our error monitoring system (like Slack channel).

6. **Testing**
    - Write unit tests for all the complex functions or classes, or the ones that are critical for the application.

7. **Code Review**
    - Always get your code reviewed by at least one peer before merging it to the dev branch.

8. **Documentation**
    - Mention the problem statement and proposed solution in the JIRA ticket and explain the architecture in the Google
      Docs.

9. **Version Control**
    - Commit Message Format: [JIRA-TICKET-ID]: Short Description of the change.
    - Branch Naming: JIRA-TICKET-ID-short-description.
    - Always create a new branch for a new feature or bug fix.
    - Always rebase your branch with the dev branch before creating a PR.
    - Always squash your commits before merging your branch to the dev branch.
    - Always delete your branch after merging it to the dev branch. Or there is auto branch deletion after the merge.
    - Explain the changes in the PR description.
    - Before assigning the PR to a reviewer, make sure all the checks are passing.
    - After merging the PR and deploying the code to the dev environment, please do a sanity check.

10. **Security**
    - Never log sensitive information like passwords, API keys, etc.
    - Always keep sensitive information in GCP Secrets Manager.
    - Always use the latest version of the libraries to avoid security vulnerabilities.

### Coding best practices

1. **Avoid Magic Numbers**
    - Avoid using magic numbers in the code. Instead, use constants with meaningful names. For example, instead of using
      1000
      in the code, use a constant named TIMEOUT.

2. **Avoid Deep Nesting**
    - Avoid deep nesting in the code. It makes the code difficult to read and understand. Instead, break the nested code
      into
      smaller functions. This will make the code more readable and maintainable. example

```typescript  
// Bad
if (condition1) {
  if (condition2) {
    if (condition3) {
      // code
    }
  }
}

// Good
if (condition1 && condition2 && condition3) {
  // code
}
```

3. **Avoid Long Functions**
    - Avoid writing long functions. Long functions are difficult to read and understand. Instead, break the long
      function into
      smaller functions. This will make the code more readable and maintainable. example

```typescript
// Bad
function longFunction() {
  // code
  // code
  // code
  // code
  // code
}

// Good
function longFunction() {
  function1();
  function2();
  function3();
}
```

4. **Avoid Duplicate Code**
    - Avoid writing duplicate code. Duplicate code makes the code difficult to maintain. Instead, create a function for
      the
      duplicate code and call the function wherever needed. example

```typescript
// Bad
const firstCircleRadius = 10;
const areaOfFirstCircle = Math.PI * firstCircleRadius * firstCircleRadius;

const secondCircleRadius = 20;
const areaOfSecondCircle = Math.PI * secondCircleRadius * secondCircleRadius;

// Good
function calculateAreaOfCircle(radius) {
  return Math.PI * radius * radius;
}

const firstCircleRadius = 10;
const areaOfFirstCircle = calculateAreaOfCircle(firstCircleRadius);

```

5. **DRY Principle**
    - Don't Repeat Yourself (DRY) principle states that every piece of knowledge must have a single, unambiguous,
      authoritative
      representation within a system. In other words, every piece of code should have a single source of truth. example

```typescript
// Bad
const firstCircleRadius = 10;
const secondCircleRadius = 20;
const areaOfFirstCircle = Math.PI * firstCircleRadius * firstCircleRadius;
const areaOfSecondCircle = Math.PI * secondCircleRadius * secondCircleRadius;


// Good
function calculateAreaOfCircle(radius) {
  return Math.PI * radius * radius;
}

const firstCircleRadius = 10;
const secondCircleRadius = 20;
const areaOfFirstCircle = calculateAreaOfCircle(firstCircleRadius);
const areaOfSecondCircle = calculateAreaOfCircle(secondCircleRadius); 
```

6. **Avoid synchronous code**
    - Avoid writing synchronous code. Synchronous code blocks the execution of the program until the current operation
      is
      completed. Instead, use asynchronous code to make the program more responsive. example

```typescript
mkdirSync('path');

// Refactored code
await mkdir('path');
```

7. **Avoid string literals**
    - Avoid using string literals in the code. Instead, use enums or constants with meaningful names. example

```typescript
// Bad
const status = 'active' || 'inactive';

// Good
enum Status {
  Active = 'active',
  Inactive = 'inactive',
}
```

8. **Return type is important**
    - Always specify the return type of a function. It makes the code more readable and maintainable. example

```typescript
// Bad
function add(a, b) {
  return a + b;
}

// Good
function add(a: number, b: number): number {
  return a + b;
}
```

9. **Use SOLID principles**
    - SOLID principles are a set of five principles that help you design well-structured, maintainable, and scalable
      software.
        - Single Responsibility Principle (SRP): A class should have only one reason to change.
        - Open/Closed Principle (OCP): A class should be open for extension but closed for modification.
        - Liskov Substitution Principle (LSP): Objects of a superclass should be replaceable with objects of its
          subclasses without affecting the functionality of the program.
        - Interface Segregation Principle (ISP): A client should not be forced to implement an interface that it does
          not
          use.
        - Dependency Inversion Principle (DIP): High-level modules should not depend on low-level modules. Both should
          depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.

10. **Use Design Patterns**
    - Design patterns are proven solutions to common problems in software design. They help you write code that is
      flexible,
      maintainable, and scalable. Some common design patterns are:
        - Singleton, Factory, Builder, Adapter, Observer, Strategy, Decorator, etc.

11. **Use Functional Programming**
    - Functional programming is a programming paradigm that treats computation as the evaluation of mathematical
      functions and
      avoids changing-state and mutable data. It makes the code more readable, maintainable, and scalable. Some
      principles of
      functional programming are:
        - Pure functions, Immutability, Higher-order functions, Recursion, etc.
          example:
      ```typescript
        // Bad
        let sum = 0;
        for (let i = 0; i < numbers.length; i++) {
          sum += numbers[i];
        }
      
        // Good
        const sum = numbers.reduce((acc, num) => acc + num, 0);
    ```

## Instructions for Freshers:

1. Please make sure no unrelated file is pushed into your PR.
2. Please make sure every field and function is properly typed and try to avoid using **any** type. example:

```typescript
// Bad
function add(a: any, b: any) {
  return a + b;
}

// Good
function add(a: number, b: number): number {
  return a + b;
}
```
