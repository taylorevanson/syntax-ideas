I sometimes do some `str = str.replace(needle, '')` too often - setting a variable by using `str = str` or `count = count`. It could be cool to do some "by reference" stuff and some eliminating of this dumb thing IMO, similar to PHP but in JS maybe?
```javascript

let str = 'test'

// if you don't do str = str
str.replace('test', 'pass')
console.log(str) // output = test

// if you do the str = str redundancy
str = str.replace('test', 'pass')
console.log(str) // output = pass

// prefix syntaxes that could shorten the str = str redundancy
&str.replace('test', 'pass')
str..replace('test', 'pass')
str:replace('test', 'pass')
str = .replace('test', 'pass')

// a few suffixes that could shorten the str = str redundancy
str.replace('test', 'pass').self
str.replace('test', 'pass').this 
str.replace('test', 'pass').let // my vote
```