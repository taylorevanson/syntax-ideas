```php
$operations = 0;
$block = {
    $operations++;
    $query->execute('INSERT INTO weapons(name) VALUES(?)', $weapon);
};

foreach(['rock', 'paper', 'scissors'] as $weapon) $block;
foreach(['gun', 'bomb', 'knife'] as $weapon) $block;

$operationsLeft = 2;
while($operationsLeft--) $block;

$operationsLeft = 3;
do $block while($operationsLeft--)
```
Basically, just be able to set code blocks as variables and use them. More handy with iteration than flow control, but here's some flow control examples.
```php
$weapon = [
    'name' => 'rock',
    'power' => 6,
    'distance' => 3
];

$increases = [
    'power' => {
        $weapon['power']++;
        $logger->info('increased power by one');
        $query->execute('UPDATE weapons SET power = power + 1 WHERE name = ?', $weapon['name']);
    },
    'distance' => {
        $weapon['distance']++;
        $logger->info('increased distance by one');
        $query->execute('UPDATE weapons SET distance = distance + 1 WHERE name = ?', $weapon['name']);
    }
];

if(rand(1, 100) % 100) $increases['power'];
foreach($increases as $key => $increase) {
    if(rand(1, 10) % 10) $increase;
}
```
I picture them as sort of "shorthand shorthand functions". They just get executed as if the block was actually located at the place it's called from. The code below is an example of little functions without the (proposed?) syntax.
```php
$weapon = [
    'name' => 'rock',
    'power' => 6,
    'distance' => 3
];

$increases = [
    'power' => function() use($weapon) {
        $weapon['power']++;
        $logger->info('increased power by one');
        $query->execute('UPDATE weapons SET power = power + 1 WHERE name = ?', $weapon['name']);
    },
    'distance' => function() use($weapon) {
        $weapon['distance']++;
        $logger->info('increased distance by one');
        $query->execute('UPDATE weapons SET distance = distance + 1 WHERE name = ?', $weapon['name']);
    }
];

if(rand(1, 100) % 100) $increases['power']();
foreach($increases as $key => $increase) {
    if(rand(1, 10) % 10) $increase();
}
```