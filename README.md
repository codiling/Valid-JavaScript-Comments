# Valid-JavaScript-Comments

function comments_correct(input) {
    // Initialize a stack to handle multi-line comments
    let stack = [];

    for (let i = 0; i < input.length; i++) {
        if (input[i] === '/' && input[i + 1] === '/') {
            // Single-line comment (//)
            i++; // Skip the next character as it's part of //
        } else if (input[i] === '/' && input[i + 1] === '*') {
            // Start of a multi-line comment (/*)
            stack.push('/*');
            i++; // Skip the next character as it's part of /*
        } else if (input[i] === '*' && input[i + 1] === '/') {
            // End of a multi-line comment (*/)
            if (stack.length === 0 || stack.pop() !== '/*') {
                return false; // No matching /* for this */
            }
            i++; // Skip the next character as it's part of */
        } else {
            // Invalid single / or unexpected character
            return false;
        }
    }

    // If the stack is empty, all multi-line comments are properly closed
    return stack.length === 0;
}

// Examples
console.log(comments_correct("//////")); // True
console.log(comments_correct("/**//**////**/")); // True
console.log(comments_correct("///*/**/")); // False
console.log(comments_correct("/////")); // False

