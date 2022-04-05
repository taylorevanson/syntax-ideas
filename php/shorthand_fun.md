I like the minimal syntax in Node. I like `new Query()` in parentheses when I can get away with it, I don't
like writing the token `function`, starting to hate commas, stuff like that. I like the shorthand map of the user to the 
`mapped` variable. That's all I need: the data in a different structure (in a situation like this).
```javascript
let mapped = {},
    users = (new Query()).select('*').from('users')
    users = users.map(user => mapped[user.id] = user)

let func = user => console.log(user.music)
users.map(func)
```
Some of the improvements to Node.js over the years can be imitated with formatting:
```php
$users = (new Query())->select('*')->from('users')
$func = function($user) { $logger->info($user->getMusic()); };
array_map($func, $users)
```
But if some of the syntax improvements could be embraced you might be able
to have it look as natural as it does in Node.js to have shorthand arrow functions
(and without parentheses).
```php
$func = $user => $logger->info($user->getMusic());
array_map($func, $users);
```
You could drop the semicolons?
```php
$func = $user => $logger->info($user->getMusic())
array_map($func, $users)
```
Combined still looks pretty clean:
```php
array_map($user => $logger->info($user->getMusic()), $users)
```
Here's some other idea syntax that's a little more radical. Letting loose a little!
```php
$func = ($op) use($operations) => {
    
}

$bootId = foreach($mapped as $id => $user) {
    if($user->booted) break $id;
}
echo $bootId; // user id, 214 or something

$test = foreach($mapped as $id => $user) {
    if(2 < 1) break TRUE;
}
echo $test; // FALSE
```