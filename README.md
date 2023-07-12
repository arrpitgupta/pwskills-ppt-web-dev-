# Create a app where you have an input box and whenever a user types something in the input box and hits submit it should be added on the webpage below the input box
<!DOCTYPE html>
<html>
<head>
</head>
<body>
  <input type="text" id="inputText" placeholder="Enter text">
  <button id="submitButton">Submit</button>
  <div id="output"></div>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      var inputText = document.getElementById("inputText");
      var submitButton = document.getElementById("submitButton");
      var output = document.getElementById("output");

      submitButton.addEventListener("click", function() {
        var text = inputText.value;
        if (text !== "") {
          var paragraph = document.createElement("p");
          paragraph.textContent = text;
          output.appendChild(paragraph);
          inputText.value = "";
        }
      });
    });
  </script>
</body>
</html>
