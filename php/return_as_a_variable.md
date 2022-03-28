An extremely common process inside of PHP functions is to set a variable at the top, add to it programmatically, and then return it in the end. There is often a single variable that the entire function revolves around. Example:
```php
function getMaxNumberOfThings($num) {
    $query = new Query();
    
    if($num > 5) $query->limit($num);
    
    $query->select('*')->from('todo');
    return $query->fetchAll();
}
```
What's the point of the `$query` variable really? It depends who you ask.
It could be cool if you could treat `return` as a variable at the start of a function. Examples:
```php
function getMaxNumberOfThings($max) {
    return = new Query();
    
    if($max > 5) return->limit($max);
    
    return->select('*')->from('todo');
    return->fetchAll(); // sets "return" as `return->fetchAll()`
}

function getNumberOfDoableThingsInNumberOfMinutes($minutes) {
    return = 0;

    foreach($todos as $todo) {
        $mins = $todo->getMinutes();
        if($mins > $minutes) break;
        $minutes -= $mins;
        return++;
    }
}

$numberOfThings = getNumberOfDoableThingsInNumberOfMinutes(60);
$things = getMaxNumberOfThings(7);
```
As I wrote this invalid yet possible syntax I realized it's really handy to remove "return" off the end of the response. Here's a bad example of the possible syntax:
```php
function getMaxNumberOfThings($max) {
    return = new Query();
    
    if($max > 5) return->limit($max);
        
    return->select('*')->from('todo');
    return = return->fetchAll(); // bad
    return; // bad
}
```
Best short example:
```php
function getTodos(): ResultSet {
    return = new Query();
    if($max > 5) return->limit($max);
    return->select('*')->from('todo')->fetchAll();
}

$todos = getTodos(8);
```

Would knowing precisely what object you are going to work on and return have some potential performance improvements?
As an intermediate developer, I wonder. 

Could it clean up the inside of a function?
If you looked at the code inside of a function, 
and you saw things happening to the "`return` variable",
would that help you to infer what's going on in the function if you know that the 
variable you're working with is the END VARIABLE?
Instead of having to look at variable names and scroll to the bottom of the
function and see which one is getting returned?