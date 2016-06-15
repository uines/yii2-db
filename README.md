Yii 2 Database Toolkit
======================

Database extensions

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist dmstr/yii2-db "*"
```

or add

```
"dmstr/yii2-db": "*"
```

to the require section of your `composer.json` file.

Commands
--------

**/!\ EXPERIMENTAL /!\**


Only include specific tables (schema & data dump) 

* `yii db/x-dump --includeTables=table_1,table,2,table_3,...`


Only include specific tables (data dump)

* `yii db/x-dump --includeTables=table_1,table,2,table_3,... --dataOnly=1`


Dump all tables excluding specific tables (schema & data dump) 

* `yii db/x-dump --excludeTables=table_1,table,2,table_3,...`


Dump all tables excluding specific tables (data dump) 

* `yii db/x-dump --excludeTables=table_1,table,2,table_3,... --dataOnly=1`



Usage
-----

### [dmstr\db\behaviors\HydratedAttributes](https://github.com/dmstr/yii2-db/blob/master/db/behaviors/HydratedAttributes.php)

Retrieves all eager loaded attributes of a model including relations. Once the extension is installed, simply use it in your code by accessing the corresponding classes by their full namespaced path.

### [dmstr\db\mysql\FileMigration](https://github.com/dmstr/yii2-db/blob/master/db/mysql/FileMigration.php)

runs database migrations from `sql` files

Create a file migration class

```
./yii migrate/create \
    --templateFile='@vendor/dmstr/yii2-db/db/mysql/templates/file-migration.php' init_dump
```

### [dmstr\console\controllers](https://github.com/dmstr/yii2-db/blob/master/console/controllers)

Include it in your console configuration

```
   'controllerMap' => [
        'db'         => [
            'class' => 'dmstr\console\controllers\MysqlController',
            'noDataTables' => [
                'app_log',
                'app_session',
            ]
        ],
    ],
```

Show help

```
./yii help db
```

Available commands
  
```
DESCRIPTION

MySQL database maintenance command.


SUB-COMMANDS

- db/create           Create MySQL database from ENV vars and grant permissions
- db/dump             Dumps current database tables to runtime folder
- db/index (default)  Displays tables in database
```

Traits
---

### [dmstr\db\traits\ActiveRecordAccessTrait](https://github.com/dmstr/yii2-db/blob/master/db/traits/ActiveRecordAccessTrait.php)

How to equip your active record model with access control

- Use update migration in `db/migrations/m160609_090908_add_access_columns`

    - set all `$tableNames` to be updated and run migration

This migrations adds the available access check columns to your database table(s)

```
'access_owner',
'access_read',
'access_update',
'access_delete',
'access_domain',
```

- Add `use \dmstr\db\traits\ActiveRecordAccessTrait;` to your active record model

- *(update your cruds)*


**:secret: Congrats, you are now ready to manage specific access checks on your active records!**

:bulb: Access options:

- All access option -> {*}
- specific rbac roles and permissions assignable
    - single or multi
        - `{*}`
        - `{Role1},{Role2},{Permission1},...`
        
- limit access to specific domains / languages
    - single or multi
        - `{*}`
        - `{de},{en},{fr},...`
        
- `Owner` access overrides other given permissions
    - every active rocord can have exact one owner!

Planned updates:
---

- ActiveRecordAccessTrait
    -  in cruds use select2 multi for inputs (domain, read, update, delete)
        - Setter: authItemArrayToString()
        - Getter: authItemStringToArray()
        

---

Built by [dmstr](http://diemeisterei.de)
