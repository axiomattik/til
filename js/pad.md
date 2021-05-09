# JavaScript's padStart and padEnd

If you have these three strings: `'1', '12', '123'` And you'd like them all to be the same length with leading zeroes, then you might do what I have been in the habit of doing for a long time and write a helper function, such as:

```
function zfill(s, targetLength) {
	while ( s.length < targetLength ) {
		s = '0' + s;
	}
	return s;
}

let strings = ['1', '12', '123']
strings.map( (s) => zfill(s, 3) );

> Array(3) [ '001', '012', '123' ]

```

But this has not been at all necessary since ECMAScript 2017, which introduced two String methods `padStart` and `padEnd` that do the same thing with a little more flexibility.

```
let strings = ['1', '12', '123']
strings.map( (s) => s.padStart(3, '0');

> Array(3) [ '001', '012', '123' ]

```

Or maybe something a little smidge more interesting:

```
let width = 9;

function updown(n) {
	let arr = new Array(n).fill(null).map( (_, i) => i+1 );
	return arr.join('') + arr.reverse().join('').substring(1);
}

let arr = new Array(width).fill(null).map(
	(_, i) => {
		let n = i+1;
		if ( n < width/2 + 1 ) return updown(n);
		return updown(width - i);
	}
);

for (let line of arr) {
	let n = parseInt(line.substring(line.length/2, line.length/2+1));
	console.log(
		line
		.padStart(width/2 + n, '0')
		.padEnd(width, '0')
	);
}
```
