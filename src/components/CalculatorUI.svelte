<script>
  export let displayText;

  const operatorKeys = {
    PLUS: "plus",
    MINUS: "minus",
    MULTIPLY: "multiply",
    DIVIDE: "divide",
    CLEAR: "clear",
    EQUAL: "equal",
  };

  const numberKeys = {
    ZERO: "zero",
    ONE: "one",
    TWO: "two",
    THREE: "three",
    FOUR: "four",
    FIVE: "five",
    SIX: "six",
    SEVEN: "seven",
    EIGHT: "eight",
    NINE: "nine",
  };

  const buttons = [
    { id: operatorKeys.PLUS, value: "+" },
    { id: operatorKeys.MINUS, value: "-" },
    { id: operatorKeys.MULTIPLY, value: "*" },
    { id: operatorKeys.DIVIDE, value: "/" },
    { id: operatorKeys.CLEAR, value: "C" },
    { id: operatorKeys.EQUAL, value: "=" },
    { id: numberKeys.ZERO, value: "0" },
    { id: numberKeys.ONE, value: "1" },
    { id: numberKeys.TWO, value: "2" },
    { id: numberKeys.THREE, value: "3" },
    { id: numberKeys.FOUR, value: "4" },
    { id: numberKeys.FIVE, value: "5" },
    { id: numberKeys.SIX, value: "6" },
    { id: numberKeys.SEVEN, value: "7" },
    { id: numberKeys.EIGHT, value: "8" },
    { id: numberKeys.NINE, value: "9" },
  ];
</script>

<div class="root">
  <div class="display">
    <span>{displayText}</span>
  </div>
  <div class="grid-container">
    {#each buttons as eachButton}
      <button class={eachButton.id}>{eachButton.value}</button>
    {/each}
  </div>
</div>

<style>
  .plus {
    grid-area: plus;
  }
  .minus {
    grid-area: minus;
  }
  .multiply {
    grid-area: multiply;
  }
  .divide {
    grid-area: divide;
  }
  .equal {
    grid-area: equal;
  }
  .clear {
    grid-area: clear;
  }
  .zero {
    grid-area: zero;
  }
  .one {
    grid-area: one;
  }
  .two {
    grid-area: two;
  }
  .three {
    grid-area: three;
  }
  .four {
    grid-area: four;
  }
  .five {
    grid-area: five;
  }
  .six {
    grid-area: six;
  }
  .seven {
    grid-area: seven;
  }
  .eight {
    grid-area: eight;
  }
  .nine {
    grid-area: nine;
  }

  .display {
    border-bottom: 1px solid #e1e8eb;
    text-align: right;
    padding: 10px;
  }

  .root {
    width: 400px;
    box-shadow: rgba(0, 0, 0, 0.05) 0px 6px 24px 0px,
      rgba(0, 0, 0, 0.08) 0px 0px 0px 1px;
  }

  .grid-container {
    display: grid;
    grid-template-areas:
      "plus minus multiply divide"
      "one two three clear"
      "four five six equal"
      "seven eight nine equal"
      "zero zero zero equal";
    gap: 10px;
    padding: 10px;
  }
</style>
