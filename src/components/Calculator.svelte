<script>
  import CalculatorUI from "./CalculatorUI.svelte";

  const actionKeys = {
    clear: "clear",
    equal: "equal",
  };

  const operatorKeys = {
    plus: "plus",
    minus: "minus",
    multiply: "multiply",
    divide: "divide",
  };

  const numberKeys = {
    zero: "zero",
    one: "one",
    two: "two",
    three: "three",
    four: "four",
    five: "five",
    six: "six",
    seven: "seven",
    eight: "eight",
    nine: "nine",
  };

  let displayText = "";
  let totalCount = "0";

  const checkIsMathExpValid = (expr) => {
    try {
      eval(expr);
      return true;
    } catch (e) {
      return false;
    }
  };

  const handleKeyPress = ({ id, value }) => {
    if (id === actionKeys.clear) {
      displayText = "";
      totalCount = "0";
      return;
    }

    if (operatorKeys[id] || id === actionKeys.equal) {
      const isValid = checkIsMathExpValid(displayText);
      if (isValid) totalCount = eval(displayText);
    }

    if (id !== actionKeys.equal) displayText = displayText + value;
  };
</script>

<CalculatorUI
  {displayText}
  {operatorKeys}
  {numberKeys}
  {totalCount}
  {actionKeys}
  {handleKeyPress}
/>
