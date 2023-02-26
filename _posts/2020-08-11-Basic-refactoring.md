---
layout: post
title: Basic refactoring
tags: programming statments C#
---

Plain statements `For` `Foreach` `While` `Do` each achieve different means to an end - but how should they be written? As in how once they be refactored in line with common dev commmunuity standards? Here is a lowdown:

# For

```csharp
for (int i = 0; i < count; i++)
{
  // Implementation
}
```

* Use short but meaningful names to represent loop variables. Use single letter variables only where the code within the 2. loop is simple and a few lines long.
* The expressions within a for statement must be separated by whitespace to aid clarity.
* Always use braces with a for loop, even if there is only one line of code within the loop.
* The loop counter must not be modified within the loop.
* The loop upper limit must not be modified within the loop.
* Avoid using the comma operator within a for loop. Instead use separate statements before the loop (for additional initialisation) and at the end of the loop (for additional iteration).
* Best Practice: try to pre-evaluate the condition expression into a variable if possible. For example: 

```csharp
for (int index = 0; index < someDataSet.SomeTable.Rows.Count; index++)
``` 

could be improved with:

```csharp
int rowCount = somedataSet.SomeTable.Rows.Count; 
for( int index = 0; index < rowCount; index++)
```

If the loop is being used to find or evaluate a particular condition, when the condition is met the loop should exit immediately using a break statement.

# Foreach

```csharp
private void DisplayNameList(string[] nameList)
{
     foreach (string name in nameList)
     {
          // display name 
     }
}
```

* Use short but meaningful names to represent loop variables. Do not use single letter variables.
* The loop variable must not be modified within the loop. 
* The array/collection being enumerated must not be modified. 
* Always use braces with a foreach loop, even if there is only one line of code within the loop. 
* If the loop is being used to find or evaluate a particular condition, when the condition is met the loop must stop using a break statement.


# While

```csharp
private void DisplayArray(string[] array)
{
    int index = 0;
    while (index < array.Length)
     {
         // display string at index         index++; 
     }
}
```

* Use for loops or foreach loops in preference to while-loops. 
* Use braces with a while-loop, even if there is only one line of code within the loop. 
* There must be a single space between the while keyword and the opening parenthesis. 
* If the loop is being used to find or evaluate a particular condition, when the condition is met the loop must stop using a break statement. 

# Do

```csharp
private void DisplayArray(string[] array)
{
     int index = 0; do
     {
       // display string at index         index++; 
     } while (index != array.Length);
}
```

* Use for loops or foreach loops in preference to do loops. 
* Use braces with a do-loop, even if there is only one line of code within the loop. 
* The while statement appears on the same line as the closing brace.

