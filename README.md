orgtbl2keepass
==============

Convert passwords.org to a KeePass database

DESCRIPTION
===========

Converts an Emacs org-mode table from the following format:

    |-------+----------+----------+----------------------+--------------|
    | Title | Username | Password | URL                  | Comment      |
    |-------+----------+----------+----------------------+--------------|
    | site1 | user1    | pw1      | http://www.site1.com | my favourite |
    | site2 | user2    | pw2      | http://example.com   |              |
    |       |          |          |                      |              |

into a KeePass database.  Can be used with any number of columns in
any order using the fields that the File::KeePass->add_entry method
understands:

    accessed => "2010-06-24 15:09:19", # last accessed date
    auto_type => [{keys => "{USERNAME}{TAB}{PASSWORD}{ENTER}", window => "Foo*"}],
    binary   => {foo => 'content'}; # hashref of filename/content pairs
    comment  => "", # a comment for the system - auto-type info is normally here
    created  => "2010-06-24 15:09:19", # entry creation date
    expires  => "2999-12-31 23:23:59", # date entry expires
    icon     => 0, # icon number for use with agents
    modified => "2010-06-24 15:09:19", # last modified
    title    => "Something",
    password => 'somepass', # will be hidden if the database is locked
    url      => "http://",
    username => "someuser",
    id       => "0a55ac30af68149f", # auto generated if needed, v1 is any hex char, v2 is any 16 char
    group    => $gid, # which group to add the entry to

The first row has to be the field name.

Create a config file ~/.orgtbl2keepassrc.json containing this:

    {
        "master_password"      : "secret",
        "password_kdb_file"    : "/home/username/path/passwords-test.kdb",
        "password_org_file"    : "/home/username/path/pw_newformat.org",
        "password_table_start" : "* websites"
    }

 - master_password      :  password for the keepass database
 - password_kdb_file    :  path and filename for the keepass database
 - password_org_file    :  path and filename for the passwords.org file
 - password_table_start :  the passwords table starts at this line/word

e.g. lines before this and after this table are ignored:

    * websites
    |-------+-----+----------+----------+---------|
    | title | URL | username | password | comment |
    |       |     |          |          |         |

REQUIREMENTS
============

File::KeePass Perl module.  Was tested with version 2.03 with Perl
v5.18.2 on Debian unstable.

TODO
====

 - Maybe use STDIN to read the org file and STDOUT to output the kdb file?
 - Use command line parameters as an alternative to the config file?
 - Use different KeePass groups, separated in different org-tables?
