# Build-a-JavaScript-Calculator https://codepen.io/nickefr-the-flexboxer/pen/GRLBWrz?editors=1111
Fulfill the below user stories and get all of the tests to pass. Use whichever libraries or APIs you need. Give it your own personal style.

User Story #1: My calculator should contain a clickable element containing an = (equal sign) with a corresponding id="equals".

User Story #2: My calculator should contain 10 clickable elements containing one number each from 0-9, with the following corresponding IDs: id="zero", id="one", id="two", id="three", id="four", id="five", id="six", id="seven", id="eight", and id="nine".

User Story #3: My calculator should contain 4 clickable elements each containing one of the 4 primary mathematical operators with the following corresponding IDs: id="add", id="subtract", id="multiply", id="divide".

User Story #4: My calculator should contain a clickable element containing a . (decimal point) symbol with a corresponding id="decimal".

User Story #5: My calculator should contain a clickable element with an id="clear".

User Story #6: My calculator should contain an element to display values with a corresponding id="display".

User Story #7: At any time, pressing the clear button clears the input and output values, and returns the calculator to its initialized state; 0 should be shown in the element with the id of display.

User Story #8: As I input numbers, I should be able to see my input in the element with the id of display.

User Story #9: In any order, I should be able to add, subtract, multiply and divide a chain of numbers of any length, and when I hit =, the correct result should be shown in the element with the id of display.

User Story #10: When inputting numbers, my calculator should not allow a number to begin with multiple zeros.

User Story #11: When the decimal element is clicked, a . should append to the currently displayed value; two . in one number should not be accepted.

User Story #12: I should be able to perform any operation (+, -, *, /) on numbers containing decimal points.

User Story #13: If 2 or more operators are entered consecutively, the operation performed should be the last operator entered (excluding the negative (-) sign). For example, if 5 + * 7 = is entered, the result should be 35 (i.e. 5 * 7); if 5 * - 5 = is entered, the result should be -25 (i.e. 5 * (-5)).

User Story #14: Pressing an operator immediately following = should start a new calculation that operates on the result of the previous evaluation.

User Story #15: My calculator should have several decimal places of precision when it comes to rounding (note that there is no exact standard, but you should be able to handle calculations like 2 / 7 with reasonable precision to at least 4 decimal places).

Note On Calculator Logic: It should be noted that there are two main schools of thought on calculator input logic: immediate execution logic and formula logic. Our example utilizes formula logic and observes order of operation precedence, immediate execution does not. Either is acceptable, but please note that depending on which you choose, your calculator may yield different results than ours for certain equations (see below example). As long as your math can be verified by another production calculator, please do not consider this a bug.

EXAMPLE: 3 + 5 x 6 - 2 / 4 =

Immediate Execution Logic: 11.5

Formula/Expression Logic: 32.5
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .calculator {
      background-color: #fff;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      width: 300px;
      max-width: 100%;
    }

    .display {
      background-color: #f2f2f2;
      padding: 10px;
      margin-bottom: 10px;
      font-size: 24px;
      text-align: right;
      border-radius: 5px;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    .button {
      padding: 10px;
      font-size: 18px;
      text-align: center;
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background-color: #ccc; /* Default grey color */
      color: #333; /* Dark text color */
    }

    .button:hover {
      background-color: #bbb; /* Darker grey on hover */
    }

    #equals {
      background-color: #007bff; /* Blue color for = */
      color: #fff; /* White text color */
    }

    #AC {
      background-color: red; /* Red color for AC */
      color: #fff; /* White text color */
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

  <script type="text/babel">
    function Calculator() {
      const [display, setDisplay] = React.useState('');

      const handleClick = (value) => {
        if (value === '=') { // User Story #9: In any order, I should be able to add, subtract, multiply and divide a chain of numbers of any length, and when I hit =, the correct result should be shown in the element with the id of display.
          try {
            setDisplay(eval(display).toString());
          } catch (error) {
            setDisplay('Error');
          }
        } else if (value === 'AC') { // User Story #7: At any time, pressing the clear button clears the input and output values, and returns the calculator to its initialized state; 0 should be shown in the element with the id of display.
          setDisplay('');
        } else if (value === '.') { // User Story #11: When the decimal element is clicked, a . should append to the currently displayed value; two . in one number should not be accepted.
          if (!display.includes('.')) {
            setDisplay(display + value);
          }
        } else {
          if (!(value === '0' && display === '0')) { // User Story #10: When inputting numbers, my calculator should not allow a number to begin with multiple zeros.
            setDisplay(display + value);
          }
        }
      };

      return (
        <div className="calculator">
          <div className="display" id="display">{display || '0'}</div>
          <div className="buttons">
            {[7, 8, 9, '+', 4, 5, 6, '-', 1, 2, 3, '*', 'AC', 0, '.', '='].map((item, index) => (
              <button className="button" key={index} id={item === '=' ? 'equals' : item === 'AC' ? 'AC' : null} onClick={() => handleClick(item)}>
                {item === 'AC' ? 'C' : item}
              </button>
            ))}
          </div>
        </div>
      );
    }

    ReactDOM.render(<Calculator />, document.getElementById('root'));
  </script>
</body>
</html>
