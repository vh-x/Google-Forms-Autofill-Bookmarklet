# Google Forms Autofill Bookmarklet

An easy bookmarklet to generate pre-filled links for Google Forms.

```javascript
javascript: void (function () {
  var d = document;
  if (d.URL.includes("/viewform")) {
    var a = d.getElementById("link");
    if (!a) {
      a = d.createElement("a");
      d.querySelector('[role="heading"]').parentElement.appendChild(a);
    }
    a.innerText = "Pre-filled Link";
    a.id = "link";
    a.href =
      d.URL.split("?")[0] +
      "?" +
      [...d.getElementsByTagName("input")]
        .filter(
          (i) =>
            i.value && (i.name.includes("entry") || i.name === "emailAddress")
        )
        .map((i) => `${i.name}=${encodeURIComponent(i.value)}`)
        .join("&");
  }
})();
```
