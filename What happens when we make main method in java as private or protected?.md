# What happens when we make main method in java as private or protected?

# Main Method Visibility in Java

In Java, the main method serves as the entry point for the application, and its correct signature must be `public static void main(String[] args)`. If you modify the visibility of the main method to private or protected, the behavior will change as follows:

## Private `main` Method:
- The program will compile successfully because Java does not enforce a specific access modifier for the main method at compile-time.
- However, when you try to run the program, the JVM will not be able to access the main method due to its private visibility.
- This will result in a runtime error, specifically a `java.lang.NoSuchMethodError: main` or `Main method not found in class <ClassName>` error message, indicating that the JVM could not find an accessible main method.

## Protected `main` Method:
- Similar to the private modifier, the program will compile without issues.
- At runtime, the JVM will also fail to access the main method due to its protected visibility, leading to the same `NoSuchMethodError` or `Main method not found in class <ClassName>` error.

## Summary:
- The main method must be public for the JVM to access and execute it. Any other visibility modifier (private, protected, or package-private) will cause a runtime error because the JVM requires the main method to be accessible publicly to serve as the entry point of the application.
