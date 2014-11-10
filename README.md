orgtbl2keepass
==============

Convert passwords.org to a KeePass database

DESCRIPTION
===========

Converts an Emacs org-mode table from the following format:

    |              |          |
    | website name | password |
    |              |          |
    | website name |          |
    | user name    | password |
    |              |          |
    | website name |          |
    | user name    | password |
    | email@addr   |          |
    |              |          |
    | website name |          |
    | email@addr   |          |
    | user name    | password |
    |              |          |

into a KeePass database.  Supported org table formats:

1) only website name and password

    |              |          |
    | website name | password |
    |              |          |

Record will be converted to:

 - title    => website name,
 - password => password

2) website name, user name, password

    |              |          |
    | website name |          |
    | user name    | password |
    |              |          |

Record will be converted to:

 - title    => website name,
 - username => user name,
 - password => password

3) website name, user name, email, password

    |              |          |
    | website name |          |
    | user name    | password |
    | email@addr   |          |
    |              |          |

Second and third line can be in any order. Record will be converted to:

 - title    => website name,
 - username => user name,
 - password => password
 - comment  => email@addr

REQUIREMENTS
============

File::KeePass Perl module.  Was tested with version 2.03 with Perl
v5.18.2 on Debian unstable.
