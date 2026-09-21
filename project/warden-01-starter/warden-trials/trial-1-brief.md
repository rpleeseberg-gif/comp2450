# Trial I — *The Foundations Brief*

*Warden of the Foundations · Midterm 1 · 15 %*

Four short answers, one from each floor above. **50–100 words per answer.** No code on this trial (except the lambdas in Q3); 
just clear thinking.

AI is welcome to *check* your answers; it is not welcome to *write your sentences*. These answers are short enough that an 
LLM voice is recognisable.

---

## 1. Floor 0 — ADT

> Your battle's "Use item" menu shows the *currently usable* items in your hero's inventory on this turn. 
Name the right ADT for that menu. Defend the choice against its closest neighbour (e.g., why `bag` instead 
of `set`, or `list` instead of `bag`).

I would argue that the best ADT for this scenario is the bag. This is promarily becuase the Bag allows for sorting 
items without needing to worry about a specific order. Essentially you could just reach in and pull out what you need. 
A deque would be useful but it's structure does not provide any advantages since the big difference is the ability to 
add and remove from both ends of the bag, not applicable in this scenario

---

## 2. Floor 1 — search & Big-O

> Your inventory is kept sorted by healing power (in this codebase an item's `value` measures its potency, so `value` 
plays the healing-power role). The player types `use Healing potion`. Linear or binary search to find it by name? Justify, 
and give the Big-O for each.

I would argue that since the inventory is sorted by healing power, a linear search (O notation O(N)) would be the ideal search 
method. In fact, due to how we are searching (By name), Binary searching o(log N) is not possible. The list is sorted by value, 
not by Name. So unless the healing value list is identical to the by name list, the linear function will always work. 

---

## 3. Floor 2 — sort & comparators

> Your "Use item" menu must be displayable sorted *either* by healing power (meaning `value`) *or* by weight. Show a one-line 
comparator (lambda) for each. One sentence on what language feature makes one `std::sort` call serve both orders.

*Note: `Item` has no healing field — an item's `value` measures its potency, so `value` plays the healing-power role here 
and in your battle.*

```cpp
// by healing power — i.e. by value
auto byValue  = [](const Item& a, const Item& b{return a.value < b.value;};

// by weight
auto byWeight = [](const Item& a, const Item& b) {rn a.weight < b.weight;};
```

C++ lambda expressions allow us to pass different comparison functions as argument to the same std::sort() call, 
allowing us to change the sort order without modifying the list itself.

---

## 4. Floor 3 — templates & exceptions

> Why does `Bag<T>` live in `Bag.h` instead of `Bag.cpp`? And: when the player types `9` for a 4-option menu, 
where in your code should the validation **throw**, and where should it **catch**?

Bag<T> lives in Bag.h because the template has to be included in the declaration of the function. Otherwise, 
you cannot switch between the data types. If a 9 was inputted for a 4 option menu, the code should throw it at the code 
between lines 58 and 65, the code is duplicated there with a const as the only difference but I am unsure as to which 
one it will be thrown from. It will be caught in BagException.h on line 28 where it will output the fact that the input 
is out of bounds.
