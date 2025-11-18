❌ Bad Code:
```javascript
function sum(){return a+b;}
```

🔍 Issues:
* ❌ **Global State Dependency:** The function implicitly relies on global variables `a` and `b`. This makes the function
non-reusable, unpredictable, and introduces side effects, as its behavior depends on external state.
* ❌ **Lack of Parameters:** A function designed to sum two numbers should accept those numbers as explicit parameters.
* ❌ **Potential `ReferenceError`:** If `a` or `b` are not defined in the global scope (or an accessible outer scope),
calling this function will result in a `ReferenceError`.
* ❌ **No Input Validation:** The function does not check the type of `a` and `b`. If they are not numbers (e.g.,
strings), the `+` operator will perform string concatenation instead of arithmetic addition (e.g., `"1" + "2"` results
in `"12"`), leading to unexpected bugs.
* ❌ **Poor Readability & Maintainability:** Without parameters, it's unclear at a glance what inputs the function
expects or how it should be used.

✅ Recommended Fix:

```javascript
/**
* Sums two numbers.
* @param {number} num1 The first number.
* @param {number} num2 The second number.
* @returns {number} The sum of the two numbers.
* @throws {TypeError} If either argument is not a number.
*/
function sum(num1, num2) {
if (typeof num1 !== 'number' || typeof num2 !== 'number') {
throw new TypeError("Both arguments must be numbers.");
}
return num1 + num2;
}

// Example usage:
// console.log(sum(5, 3)); // Output: 8
// console.log(sum(10, -2)); // Output: 8
// try {
// sum(1, "2"); // Throws TypeError
// } catch (error) {
// console.error(error.message); // Output: Both arguments must be numbers.
// }
```

💡 Improvements:
* ✔ **Explicit Parameters:** `num1` and `num2` are passed as arguments, making the function's inputs clear and promoting
reusability.
* ✔ **Input Validation:** Checks if both arguments are numbers, preventing unexpected type coercion issues and throwing
a `TypeError` for invalid inputs. This makes the function robust and predictable.
* ✔ **Enhanced Readability:** The function signature immediately tells the developer what inputs are expected.
* ✔ **Improved Maintainability:** The function is self-contained and does not rely on external, unpredictable state.
* ✔ **JSDoc Comments:** Added clear documentation explaining the function's purpose, parameters, return value, and
potential errors, which is crucial for larger codebases.

✅ Further Improvement (for summing an arbitrary number of values):

If the intent is to sum an arbitrary number of values, consider using the rest parameter syntax with `reduce`:

```javascript
/**
* Sums an arbitrary number of numeric values.
* @param {...number} numbers Any number of numeric arguments to sum.
* @returns {number} The total sum of all provided numbers.
* @throws {TypeError} If any argument is not a number.
*/
function sumAll(...numbers) {
for (const num of numbers) {
if (typeof num !== 'number') {
throw new TypeError("All arguments must be numbers.");
}
}
return numbers.reduce((total, current) => total + current, 0);
}

// Example usage:
// console.log(sumAll(1, 2, 3)); // Output: 6
// console.log(sumAll(10, 20, -5, 1)); // Output: 26
// try {
// sumAll(1, 2, "three"); // Throws TypeError
// } catch (error) {
// console.error(error.message); // Output: All arguments must be numbers.
// }
```