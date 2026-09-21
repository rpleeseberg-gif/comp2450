# Trial II — *The Critique*

*Warden of the Foundations · Midterm 1 · 15 %*

This trial **requires** you to use an LLM. You will paste the prompt and the reply, then critique what you got. 
Reading and judging AI output is part of the job now; we are practicing it on purpose.

---

## The prompt

Open Claude (or your LLM of choice) and paste **this exact prompt**:

> *Write a C++ function template that returns the largest element of a `std::vector<T>`. Handle the case where the vector is 
empty. Briefly explain your design choices.*

Tell us which tool you used and the date: Copilot Chat on 2026-09-17

---

## The LLM's reply

Paste the **full reply**, code and prose. Use a fenced code block for the code. Do not edit the reply — we want to see what 
you actually got.

```cpp
// #include <vector>
#include <stdexcept>

template <typename T>
const T& largestElement(const std::vector<T>& vec) {
    if (vec.empty()) {
        throw std::runtime_error("Cannot find largest element in an empty vector");
    }

    const T* largest = &vec[0];

    for (const T& item : vec) {
        if (item > *largest) {
            largest = &item;
        }
    }

    return *largest;
}
```

Design choices:

A function template allows the function to work with any type T that supports the > operator.
The function throws an exception when the vector is empty because there is no valid largest element to return.
Returning a const reference avoids copying potentially large objects and prevents accidental modification of the element.
A simple loop is used to compare elements and track the current largest value, keeping the implementation efficient with O(n) 
time complexity.

---

## My critique  *( ≥ 150 words )*

Your critique must read like an engineer reviewing a colleague's pull request — specific, technical, and naming exactly what 
the LLM did. A vague critique ("looks fine to me, but it could be better") is *not* full credit even if the LLM's code was great.

Address each of these:

- **Compile.** Did you actually try to compile and run the code? On what types? What happened?
- **Empty case.** What does the empty-vector case actually do in this code? Is the LLM's choice reasonable? Is it different 
from what *you* would have chosen?
- **Requirements on `T`.** What does the code require of `T`? What happens if you instantiate it with a type that doesn't 
support `<` (e.g., a custom struct)?
- **Const-correctness.** Pass by value or by reference? Return by value or by reference? Would you change either?
- **`std::max_element`?** Did the LLM cheat by using the algorithm header, or did it write the loop? Which would *you* have 
shipped, and why?
- **One concrete improvement.** Name one specific change you would make before merging this into a real project. Not "make 
it better" — a concrete code change.

I have not attempted to compile this code. I was actually looking for where it might go in this code but was unsuccessful 
in finding where it is supposed to go in here if I wanted to test it. From the looks of it, the code appears to be sound. 
In this code, the empty case simply throws the error message when it is passed an empty vector. For T, the code requires 
T to be the same type as in the vector. From the looks of it, the code here allows for T to automatically be the same type 
as the passed vector since the phrase vector<T> exists. If you initiate the vector with a custom struct, the code would fail 
to compile because the custom struct would not be able to work with the < > symbols. This is a pass by reference variable and 
the code returns a const reference from the looks of it. I don't think I would change this solely becuase the logic behind it 
is sound in the sense that it handles any edge case where we might accidentally modify the element. It looks like the LLM wrote 
the loop. I would have shipped the loop and that is because it makes more sense to me in terms of understanding the code. One 
change I would have made would actually be changing the loop. I often forget about the for loops and would have probably run 
an if loop because it is what is familliar to me.
