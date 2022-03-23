#Examples:
### Javascript
import fs from "fs"
let file, path = './test.txt'

// assert that there is no file there
try fs.deleteFile(path)

// don't throw an error if it doesn't find a file
try file = fs.readFile(path)
console.log(file) // null

// no brackets on catch blocks with one statement in them
try file = fs.readFile(path) catch(e) file = fs.readFile('./default.txt')
console.log(file) // contents of ./default.txt

// arrow function-ify catch blocks
const errorHandler = (e) => {
    newrelic.sendError(e)
    throw e
}
try file = fs.readFile(path) catch errorHandler
try file = fs.readFile(path) catch (e) => {
    newrelic.sendError(e)
    console.error(e)
    file = null
}
try file = fs.readFile(path) catch e => {
    //...
}
try file = fs.readFile(path) catch e => newrelic.sendError(e)
try file = fs.readFile(path) catch e => errorHandler(e, path)

### PHP
// todo