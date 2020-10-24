Scripts for testing programming problem solutions.

## Usage

### `rr <source> [memory-limit]`
Will compile and run the `source` (C++17, Java or Python3).
The `memory-limit` is in MBs (default: 256).


### `tt <solution>`
If `input.txt` exists, will do:
```bash
rr solution <input.txt >stdout.txt
```
and if `output.txt` exists, will do:
```bash
diff stdout.txt output.txt
```

Otherwise, if `tests.txt` exists, will extract each test case into `input.txt` and `output.txt`, and will do:
```bash
tt solution
```

The `tests.txt` should look like:
```
input:
...
output:
...

input:
...
output:
...
```

Tip: the following bookmarklet scrapes sample tests from [codeforces.com](http://codeforces.com/) problem statement and downloads them in a `tests.txt` file:
```js
javascript:
var inputs = document.querySelectorAll('.input pre');
var outputs = document.querySelectorAll('.output pre');

var data = '';
for (var i = 0; i < inputs.length; i++) {
    data += 'input:\n' + inputs[i].innerText.replace(/\n*$/, '\n');
    data += 'output:\n' + outputs[i].innerText.replace(/\n*$/, '\n\n');
}

var a = document.createElement('a');
a.setAttribute('href', 'data:text/plain,' + encodeURIComponent(data));
a.setAttribute('download', 'tests.txt');
document.body.appendChild(a);
a.click();
```


### `tt <solution> <generator>`
Will do:
```bash
while true; do
  rr generator >input.txt
  tt solution
done
```


### `tt <solution> <generator> <solver>`
Will do:
```bash
while true; do
  rr generator >input.txt
  rr solver <input.txt >output.txt
  tt solution
done
```


### `dbg <source>`
Will compile the `source` (C++17) and start `gdb`.

