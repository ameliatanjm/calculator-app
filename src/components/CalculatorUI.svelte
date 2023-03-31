<script>
  export let displayText;
  export let totalCount;
  export let operatorKeys;
  export let numberKeys;
  export let actionKeys;
  export let handleKeyPress;

  const buttons = [
    { id: operatorKeys.plus, value: "+" },
    { id: operatorKeys.minus, value: "-" },
    { id: operatorKeys.multiply, value: "*" },
    { id: operatorKeys.divide, value: "/" },
    { id: actionKeys.clear, value: "AC" },
    { id: actionKeys.equal, value: "=" },
    { id: numberKeys.zero, value: "0" },
    { id: numberKeys.one, value: "1" },
    { id: numberKeys.two, value: "2" },
    { id: numberKeys.three, value: "3" },
    { id: numberKeys.four, value: "4" },
    { id: numberKeys.five, value: "5" },
    { id: numberKeys.six, value: "6" },
    { id: numberKeys.seven, value: "7" },
    { id: numberKeys.eight, value: "8" },
    { id: numberKeys.nine, value: "9" },
  ];
</script>

<div class="root">
  <div class="display">
    <div>{displayText}</div>
    <div>{totalCount}</div>
  </div>
  <div class="grid-container">
    {#each buttons as eachButton}
      <button class={eachButton.id} on:click={() => handleKeyPress(eachButton)}
        >{eachButton.value}</button
      >
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
