A class to pivot tables in PHP

Usage examples:

pivot on 'host'
```
$data = Pivot::factory($recordset)
    ->pivotOn(array('host'))
    ->addColumn(array('year', 'month'), array('users', 'clicks',))
    ->fetch();
```

pivot on 'host' with totals
```
$data = Pivot::factory($recordset)
    ->pivotOn(array('host'))
    ->addColumn(array('year', 'month'), array('users', 'clicks',))
    ->fullTotal()
    ->lineTotal()
    ->fetch();
```

pivot on 'host' and 'country'
```
$data = Pivot::factory($recordset)
    ->pivotOn(array('host', 'country'))
    ->addColumn(array('year', 'month'), array('users', 'clicks',))
    ->fullTotal()
    ->pivotTotal()
    ->lineTotal()
    ->fetch();
```

pivot on 'host' and 'country' with calculated columms
```
$averageCbk = function($reg)
{
    return round($reg['clicks']/$reg['users'],2);
};

$data = Pivot::factory($recordset)
    ->pivotOn(array('host', 'country'))
    ->addColumn(array('year', 'month'), array('users', 'clicks', Pivot::callback('average', $averageCbk)))
    ->lineTotal()
    ->pivotTotal()
    ->fullTotal()
    ->typeMark()
    ->fetch();
```

pivot on ‘host’ and ‘country’ with group count
```
$data = Pivot::factory($recordset)
    ->pivotOn(array('host', 'country'))
    ->addColumn(array('year', 'month'), array('users', 'clicks', Pivot::count('count')))
    ->fullTotal()
    ->pivotTotal()
    ->lineTotal()
    ->fetch();
```

The original recordset:
```
$recordset = array(
    array('host' => 1, 'country' => 'fr', 'year' => 2010, 'month' => 1, 'clicks' => 123, 'users' => 4),
    array('host' => 1, 'country' => 'fr', 'year' => 2010, 'month' => 2, 'clicks' => 134, 'users' => 5),
    array('host' => 1, 'country' => 'fr', 'year' => 2010, 'month' => 3, 'clicks' => 341, 'users' => 2),
    array('host' => 1, 'country' => 'es', 'year' => 2010, 'month' => 1, 'clicks' => 113, 'users' => 4),
    array('host' => 1, 'country' => 'es', 'year' => 2010, 'month' => 2, 'clicks' => 234, 'users' => 5),
    array('host' => 1, 'country' => 'es', 'year' => 2010, 'month' => 3, 'clicks' => 421, 'users' => 2),
    array('host' => 1, 'country' => 'es', 'year' => 2010, 'month' => 4, 'clicks' => 22,  'users' => 3),
    array('host' => 2, 'country' => 'es', 'year' => 2010, 'month' => 1, 'clicks' => 111, 'users' => 2),
    array('host' => 2, 'country' => 'es', 'year' => 2010, 'month' => 2, 'clicks' => 2,   'users' => 4),
    array('host' => 3, 'country' => 'es', 'year' => 2010, 'month' => 3, 'clicks' => 34,  'users' => 2),
    array('host' => 3, 'country' => 'es', 'year' => 2010, 'month' => 4, 'clicks' => 1,   'users' => 1),
);
```