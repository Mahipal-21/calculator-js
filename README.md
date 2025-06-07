const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

function askQuestion(query) {
  return new Promise((resolve) => rl.question(query, resolve));
}

async function runCalculator() {
  let continueCalculation;

  do {
    const num1Input = await askQuestion("Enter the first number: ");
    const num1 = Number(num1Input);

    const num2Input = await askQuestion("Enter the second number: ");
    const num2 = Number(num2Input);

    const operator = await askQuestion("Enter an operator (+, -, *, /): ");

    let result;

    if (operator === "+") {
      result = num1 + num2;
    } else if (operator === "-") {
      result = num1 - num2;
    } else if (operator === "*") {
      result = num1 * num2;
    } else if (operator === "/") {
      if (num2 === 0) {
        result = "Error: Cannot divide by zero.";
      } else {
        result = num1 / num2;
      }
    } else {
      result = "Invalid operator.";
    }

    console.log("Result: " + result);

    continueCalculation = (await askQuestion("Do you want to calculate again? (yes/no): ")).toLowerCase();

  } while (continueCalculation === "yes");

  rl.close();
}

runCalculator();
