# Config
A configuration file is required to start YACRS. This config file must
exist in `/web/src/config.php`. A sample config file can be found in
`/web/src/sample.config.php`. Copy sample.config.php to config.php and
change any required configuration options. An overview of the config
file can be found [here](config.md).

A sample config file is listed below:

    <?php
    $config = [];

    $config["version"]                       = "2.0.0";
    $config["title"]                         = "YACRS";
    $config["baseUrl"]                       = isset($_SERVER['HTTPS']) ? "https" : "http" . "://" . $_SERVER['HTTP_HOST'] . "/";
    $config["login"]["type"]                 = "some";

    // Whether user's can register new accounts (Only for native login system)
    $config["login"]["register"]             = true;

    $config["datetime"]["date"]["short"]     = "d/m/y";
    $config["datetime"]["date"]["long"]      = "d F Y \\a\\t";
    $config["datetime"]["time"]["short"]     = "H:i";
    $config["datetime"]["time"]["long"]      = "H:i";
    $config["datetime"]["datetime"]["short"] = $config["datetime"]["date"]["short"] . " " . $config["datetime"]["time"]["short"];
    $config["datetime"]["datetime"]["long"]  = $config["datetime"]["date"]["long"] . " " . $config["datetime"]["time"]["long"];

    // Get database details from docker
    $config["database"]["host"]              = getenv("MYSQL_HOST");
    $config["database"]["username"]          = getenv("MYSQL_USER");
    $config["database"]["password"]          = getenv("MYSQL_PASSWORD");
    $config["database"]["name"]              = getenv("MYSQL_DATABASE");

    // Basic LDAP details
    $config["ldap"]["host"]                  = "130.209.13.173";
    $config["ldap"]["context"]               = "o=Gla";

    // Manual username password combos. Used for initial setting up of admin users.
    $config["user"]["users"]["admin"]        = "dufbYqFuU4EV8WgE";

    // Users who should always be admin
    $config["user"]["admin"][0]               = "admin";

    // Details used for LDAP bind
    //$config["ldap"]["bind"]["user"] = "";
    //$config["ldap"]["bind"]["pass"] = "";

    // LDAP fields and values that result in sessionCreator (teacher) status
    $config["ldap"]["sessionCreatorRules"]   = array();
    $config["ldap"]["sessionCreatorRules"][] = array("field" => "dn", "contains" => "ou=staff");
    $config["ldap"]["sessionCreatorRules"][] = array("field" => "homezipcode", "match" => "PGR");
    $config["ldap"]["sessionCreatorRules"][] = array("field" => "uid", "regex" => "/^[a-z]{2,3}[0-9]+[a-z]$/");
    //$config["ldap"]["sessionCreatorRules"][] = array('field'=>'mail', 'regex'=>'/[a-zA-Z]+\.[a-zA-Z]+.*?@glasgow\.ac\.uk/');

    $config["baseDir"] = dirname(dirname(__FILE__));

Below is a table explaining the use of every variable in this config file.

| Variable Name                             | Description |
|-------------------------------------------|-------------|
|`$config["version"]`                       | The application version
|`$config["title"]`                         | The application title
|`$config["baseUrl"]`                       | The url to the home page of the app. E.g. http://127.0.0.1:4000/ or https://yacrs.com/ config above gets this from the request.                                               |
|`$config["login"]["type"]`                 | The login type to use. This can be: ########################
|`$config["login"]["register"]`             | Whether registration is enabled. Only for native login type.
|`$config["datetime"]["date"]["short"]`     | The format string to use for short dates
|`$config["datetime"]["date"]["long"]`      | The format string to use for long dates
|`$config["datetime"]["time"]["short"]`     | The format string to use for short times
|`$config["datetime"]["time"]["long"]`      | The format string to use for long times
|`$config["datetime"]["datetime"]["short"]` | The format string to use for short date times
|`$config["datetime"]["datetime"]["long"]`  | The format string to use for lon date times
|`$config["database"]["host"]`              | The database hostname. The configuration above uses the environmental variables to get docker config.
|`$config["database"]["username"]`          | The database username. The configuration above uses the environmental variables to get docker config.
|`$config["database"]["password"]`          | The database password. The configuration above uses the environmental variables to get docker config.
|`$config["database"]["name"]`              | The database name. The configuration above uses the environmental variables to get docker config.
|`$config["ldap"]["host"]`                  | The ldap hostname. Only used for ldap login.
|`$config["ldap"]["context"]`               | The ldap context. Only used for ldap login.
|`$config["ldap"]["sessionCreatorRules"]`   | Ldap rules to determine whether user is session creator (e.g. staff). Example above. Only used for ldap login.
|`$config["user"]["users"]`                 | Dictionary of manually entered usernames and passwrod combos. Key is username, value is password
|`$config["user"]["admin"]`                 | Array of users who should always be admin
|`$config["baseDir"]`                       | The base directory of the project
