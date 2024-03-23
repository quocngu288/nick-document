```js
downloadFile(data, fileName) {
  // const bom = new Uint8Array([
  //   parseInt("EF", 16),
  //   parseInt("BB", 16),
  //   parseInt("BF", 16),
  // ]);

  // const finalData = new Uint8Array([...bom, ...new Uint8Array(data)]);

  const finalData = new Uint8Array([...new Uint8Array(data)]);

  const blob = new Blob([finalData], { type: "text/csv" });

  const url = window.URL.createObjectURL(blob);
  const newFileNameExport = [fileName + this.$moment().format("YYYYMMDD")];

  if (navigator.msSaveOrOpenBlob) {
    navigator.msSaveBlob(blob, `${newFileNameExport}.csv`);
  } else {
    const a = document.createElement("a");
    a.href = url;
    a.download = `${newFileNameExport}.csv`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
  }
  window.URL.revokeObjectURL(url);
},
```
