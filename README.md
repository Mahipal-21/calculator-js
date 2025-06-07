// Importing the 'readline' module to take input from the command line
const readline = require('readline');

// Creating an interface for input and output using readline
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// This function asks a question and returns a Promise with the user's input
function askQuestion(query) {
  return new Promise((resolve) => rl.question(query, resolve));
}

// Main async function to run the calculator
async function runCalculator() {
  let continueCalculation;

  // Do-while loop to keep the calculator running until the user says "no"
  do {
    // Asking the user to enter the first number
    const num1Input = await askQuestion("Enter the first number: ");
    const num1 = Number(num1Input); // Converting string input to number

    // Asking the user to enter the second number
    const num2Input = await askQuestion("Enter the second number: ");
    const num2 = Number(num2Input); // Converting string input to number

    // Asking the user to choose an operator
    const operator = await askQuestion("Enter an operator (+, -, *, /): ");

    let result; // Variable to store the result

    // Performing calculation based on the selected operator
    if (operator === "+") {
      result = num1 + num2;
    } else if (operator === "-") {
      result = num1 - num2;
    } else if (operator === "*") {
      result = num1 * num2;
    } else if (operator === "/") {
      // Handling division by zero
      if (num2 === 0) {
        result = "Error: Cannot divide by zero.";
      } else {
        result = num1 / num2;
      }
    } else {
      result = "Invalid operator."; // Handling invalid operator input
    }

    // Printing the result
    console.log("Result: " + result);

    // Asking the user if they want to continue
    continueCalculation = (await askQuestion("Do you want to calculate again? (yes/no): ")).toLowerCase();

  } while (continueCalculation === "yes"); // Loop continues only if user inputs "yes"

  // Closing the readline interface
  rl.close();
}

// Starting the calculator
runCalculator();
