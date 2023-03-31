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
  let allRecords = [];
  let db = null;

  databaseOpen(function () {
    getAllRecords();
    console.log("The database has been opened");
  });

  function databaseOpen(callback) {
    const request = indexedDB.open("CalculatorAppDb", 1);

    request.onupgradeneeded = function (e) {
      db = e.target.result;
      db.createObjectStore("history", { keyPath: "timeStamp" });
    };

    request.onsuccess = function (e) {
      db = e.target.result;
      callback();
    };
    request.onerror = () => {};
  }

  const addRecords = (_displayText) => {
    const newRecord = { text: _displayText, timeStamp: Date.now() };
    const transaction = db.transaction(["history"], "readwrite");
    const store = transaction.objectStore("history");
    store.put(newRecord);
    getAllRecords();
  };

  const getAllRecords = () => {
    const transaction = db.transaction(["history"], "readonly");
    const store = transaction.objectStore("history");

    const keyRange = IDBKeyRange.lowerBound(0);
    const cursorRequest = store.openCursor(keyRange);
    let data = [];
    cursorRequest.onsuccess = function (e) {
      let result = e.target.result;

      if (result) {
        data.push(result.value);
        result.continue();
      } else {
        allRecords = data;
      }
    };
  };

  const checkIsMathExpValid = (expr) => {
    try {
      const res = eval(expr);
      return res ? true : false;
    } catch (e) {
      return false;
    }
  };

  const handleKeyPress = ({ id, value }) => {
    const isValid = checkIsMathExpValid(displayText);

    if (id === actionKeys.clear) {
      displayText = "";
      totalCount = "0";
      return;
    }

    if (operatorKeys[id] || id === actionKeys.equal) {
      if (isValid) totalCount = eval(displayText);
    }

    if (id !== actionKeys.equal) {
      displayText = displayText + value;
    } else {
      isValid && addRecords(`${displayText} = ${totalCount}`);
    }
  };
</script>

<CalculatorUI
  {displayText}
  {operatorKeys}
  {numberKeys}
  {totalCount}
  {actionKeys}
  {allRecords}
  {handleKeyPress}
/>
