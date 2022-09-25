---
title: "Phpunit Basic Study"
excerpt: "Unit Test. Phpunit 6.5 Guide 정리"

categories:
  - Repost
# tags:
#   - [tag1, tag2]

permalink: /unit-test/phpunit/6.5/

toc: true
toc_sticky: true

date: 2022-09-25
last_modified_at: 2022-09-25
---

### 🧩 <b>Code Coverage Analysis</b>
#### <span style="background-color:#fff5b1;"><b>Whitelisting Files</b></span>
> `addUncoveredFilesFromWhitelist="true"`

- 테스트되지 않은 파일을 포함할 수 있는 설정

<br>

#### <span style="background-color:#fff5b1;"><b>Whitelisting Files</b></span>
- 코드 검사 중에 테스트X, 무시하고자 하는 블록 설정하기

``` php
use PHPUnit\Framework\TestCase;

/**
 * @codeCoverageIgnore
 */
class Foo
{
  public function bar() {}
}


class Foo
{
  /**
   * @codeCoverageIgnore
   */
  public function bar() {}
}


if (false) {
  // @codeCoverageIgnoreStart
  print '*';
  // @codeCoverageIgnoreEnd
}

exit; // @codeCoverageIgnore
```

#### <span style="background-color:#fff5b1;"><b>Specifying Covered Methods</b></span>
- `@cover` : 어떤 테스트를 하려는지 지정할 때 사용하는 주석

```php
use PHPUnit\Framework\TestCase;

class BankAccountTest extends TestCase
{
  protected $ba;

  protected function setUp()
  {
    $this->ba = new BankAccount;
  }

  /** @covers BankAccount::getBalance */
  public function testBalanceIsInitiallyZero()
  {
    $this->assertEquals(0, $this->ba->getBalance());
  }

  /** @covers BankAccount::withdrawMoney */
  public function testBalanceCannotBecomeNegative()
  {
    try {
      $this->ba->withdrawMoney(1); 
    }
    catch (BankAccountException $e) {
      $this->assertEquals(0, $this->ba->getBalance());
      return;
    }
    $this->fail();
  }

  /** @covers BankAccount::depositMoney */
  public function testBalanceCannotBecomeNegative2()
  {
    try {
      $this->ba->depositMoney(-1);
    }
    catch (BankAccountException $e) {
      $this->assertEquals(0, $this->ba->getBalance());
      return;
    }
    $this->fail();
  }

  /**
   * @covers BankAccount::getBalance
   * @covers BankAccount::depositMoney
   * @covers BankAccount::withdrawMoney
   */ 
  public function testDepositWithdrawMoney()
  {
    $this->assertEquals(0, $this->ba->getBalance());
    $this->ba->depositMoney(1);
    $this->assertEquals(1, $this->ba->getBalance());
    $this->ba->withdrawMoney(1);
    $this->assertEquals(0, $this->ba->getBalance());
  }
}
```

- `@coversNoting` : 주석으로 테스트가 어떤 메서드도 사용하지 않도록 지정하기

```php
use PHPUnit\Framework\TestCase;

class GuestbookIntegrationTest extends PHPUnit_Extensions_Database_TestCase
{
  /** @coversNothing */
  public function testAddEntry()
  {
    $guestbook = new Guestbook();
    $guestbook->addEntry("suzy", "Hello world!");

    $queryTable = $this->getConnection()->createQueryTable(
      'guestbook', 'SELECT * FROM guestbook'
    );

    $expectedTable = $this->createFlatXmlDataSet("expectedBook.xml")
                          ->getTable("guestbook");
    
    $this->assertTablesEqual($expectedTable, $queryTable);
  }
}
```

### 🧩 <b>DataBase Testing</b>
#### <span style="background-color:#fff5b1;"><b>Configuration of a PHPUnit Database TestCase</b></span>

```php
use PHPUnit\Framework\TestCase;

class MyTest extends TestCase
{
  public function testCalculate()
  {
    $this->assertEquals(2, 1 + 1);
  }
}
```

> DBUnit

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

class MyGuestbookTest extends TestCase
{
  use TestCaseTrait;

  /** @return PHPUnit_Extensions_Database_DB_IDatabaseConnection */
  public function getConnection()
  {
    $pdo = new PDO('sqlite::memoery:');
    return $this->createDefaultDBConnection($pdo, ':memory:');
  }

  /** @return PHPUnit_Extensions_Database_DataSet_IDataSet */
  public function getDataSet()
  {
    return $this->createFlatXMLDataSet(dirname(__FILE__).'/_files/guestbook-seed.xml');
  }
}
```

---

#### <span style="background-color:#fff5b1;"><b>Tip: Use your own Abstract Database TestCase</b></span>

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

abstract class MyApp_Tests_DatabaseTestCase extends TestCase
{
  use TestCaseTrait;

  // only instantiate pdo once for test clean-up/fixture load
  static private $pdo = null;

  // only instantiate PHPUnit_Extensions_Database_DB_IDatabaseConnection once per test
  private $conn = null;

  final public function getConnection()
  {
    if ($this->conn === null) {
      if (self::$pdo == null) {
        self::$pdo = new PDO('sqlite::memory:');
      }
      $this->conn = $this->createDefaultDBConnection(self::$pdo, ':memory:');
    }
    return $this->conn;
  }
}
```

```xml
<!--phpuni.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<phpunit>
  <php>
    <var name="DB_DSN" value="mysql:dbname=myguestbook;host=localhost"/>
    <var name="DB_USER" value="user"/>
    <var name="DB_PASSWD" value="passwd"/>
    <var name="DB_DBNAME" value="myguestbook"/>
  </php>
</phpunit>
```

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

abstract class Generic_Tests_DatabaseTestCase extends TestCase
{
  use TestCaseTrait;

  // only instantiate pdo once for test clean-up/fixture load
  static private $pdo = null;

  // only instantiate PHPUnit_Extensions_Database_DB_IDatabaseConnection once per test
  privaet $conn = null;

  final public function getConnection()
  {
    if ($this->conn === null) {
      if (self::$pdo == null) {
        self::$pdo = new PDO( $GLOBALS['DB_DSN'], $GLOBALS['DB_USER'], $GLOBALS['DB_PASSWD']);
      }
      $this->conn = $this->createDefaultDBConnection(self::$pdo, $GLOBALS['DB_DBNAME']);
    }
    return $this->conn;
  }
}
```

<br>


### 🧩 <b>Understanding DataSets and DataTablese</b>
#### <span style="background-color:#fff5b1;"><b>Flat XML DataSet</b></span>
``` xml
<?xml version="1.0"?>
<dataset>
  <guestbook id="1" content="Hello buddy!" user="joe" created="2010-04-24 17:15:23"/>
  <guestbook id="2" content="I like it!" user="nancy" created="2010-04-26 12:14:20"/>
</dataset>
```

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

class MyTestCase extends TestCase
{
  use TestCaseTrait;

  public function getDataSet()
  {
    return $this->createFlatXmlDataSet('myFlatXmlFixture.xml');
  }
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>XML DataSet</b></span>
```xml
<?xml version="1.0"?>
<dataset>
  <table name="guestbook">
    <column>id</column>
    <column>content</column>
    <column>user</column>
    <column>created</column>
    <row>
      <value>1</value>
      <value>Hello buddy!</value>
      <value>joe</value>
      <value>2010-04-24 17:15:23</value>
    </row>
    <row>
      <value>2</value>
      <value>I like it!</value>
      <null />
      <value>2010-04-26 12:14:20</value>
    </row>
  </table>
</dataset>
```

<br>

#### <span style="background-color:#fff5b1;"><b>MySQL XML DataSet</b></span>
```
mysqldump --xml -t -u [username] --password=[password] [database] > /path/to/file.xml
```

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

class MyTestCase extends TestCase
{
  use TestCaseTrait;

  public function getDataSet()
  {
    return $this->createMySQLXMLDataSet('/path/to/file.xml');
  }
}

```

<br>

#### <span style="background-color:#fff5b1;"><b>YAML DataSet</b></span>
```yml
guestbook:
  -
    id: 1
    content: "Hello buddy!"
    user: "joe"
    created: 2010-04-24 17:15:23
  -
    id: 2
    content: "I like it!"
    user:
    created: 2010-04-26 12:14:20
```

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

class MyTestCase extends TestCase
{
  use TestCaseTrait;

  protected function getDataSet()
  {
    return new YamlDataSet(dirname(__FILE__)."/_files/guestbook.yml");
  }
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>CSV DataSet</b></span>

```csv
id,content,user,created
1,"Hello buddy!","joe","2010-04-24 17:15:23"
2,"I like it!","nancy","2010-04-26 12:14:20"
```

```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;
use PHPUnit\DbUnit\DataSet\CsvDataSet;

class CsvGuestbookTest extends TestCase
{
  use TestCaseTrait;

  protected function getDataSet()
  {
    $dataSet = new CsvDataSet();
    $dataSet->addTable('guestbook',
                        dirname(__FILE__)."/_files/guestbook.csv");
    return $dataSet;
  }
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>Database (DB) DataSet</b></span>
```php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

class MySqlGuestbookTest extends TestCase
{
  use TestCaseTrait;
  
  /** @return PHPUnit_Extensions_Database_DB_IDatabaseConnection */
  public function getConnection()
  {
    $database = 'my_database';
    $user = 'my_user';
    $password = 'my_password';
    $pdo = new PDO('mysql:...', $user, $password);
    return $this->createDefaultDBConnection($pdo, $database);
  }

  public function testGuestbook()
  {
    $dataSet = $this->getConnection()->createDataSet();
    // ...
  }

  public function testFilteredGuestbook()
  {
    $tableNames = ['guestbook'];
    $dataSet = $this->getConnection()->createDataSet($tableNames);
    // ...
  }
}
```

#### <span style="background-color:#fff5b1;"><b>Replacement DataSet</b></span>
```xml
<?xml version="1.0" ?>
<dataset>
    <guestbook id="1" content="Hello buddy!" user="joe" created="2010-04-24 17:15:23" />
    <guestbook id="2" content="I like it!" user="##NULL##" created="2010-04-26 12:14:20" />
</dataset>
```

```php
<?php
use PHPUnit\Framework\TestCase;
use PHPUnit\DbUnit\TestCaseTrait;

class ReplacementTest extends TestCase
{
  use TestCaseTrait;

  public function getDataSet()
  {
    $ds = $this->createFlatXmlDataSet('myFlatXmlFixture.xml');
    $rds = new PHPUnit_Extensions_Database_DataSet_ReplacementDataSet($ds);
    $rds->addFullReplacement('##NULL##', null);
    return $rds;
  }
}
```

<br>

(--datasetFilter부터 시작--)

---

### 🧩 <b>참고자료</b>

- [Phpunit 6.5 Guide](https://devdocs.io/phpunit~6/)