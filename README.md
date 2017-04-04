# ace
Admin Control Execution

ace v3.0

To copy a file to multiple machines:
        ace --group linux --copy_to <file> -d <remote directory>

        ace will create the specified remote directory on each host, if missing.
        If no destination is specified, the current working directory will be used.

To copy a file from multiple machines:
        ace -g webservers --copy_from <remote/path/file> -d <directory>

        ace will create a new directory for each host in the destination directory.
        If no destination is specified, the current working directory will be used.

To remotely run <command> on multiple machines:
        ace --group redhat -e <command>

        ace will read the default config file (or your specified one) to get the
        groups/hosts to utilize.

To view the lists of configured hosts:
        ace -l

Examples:
     ace -g database --copy_to buh.dat -d /opt/gecko/
     ace --group fe_web --copy_from /opt/gecko/buh.dat --destination /reports/
     ace --group all -e uptime
Commands can be stacked, "copy_to" runs first, "exec" runs second, "copy_from" runs last
     ace -g linux+ssh --exec "/tmp/test.sh;uptime" --copy_to test.sh -d /tmp
This will copy "test.sh" to "/tmp", run the copied file and then execute "uptime"


    --------------------------------------------------------------

        Options -
          --config <file>       : Alternate configuration file (default: /path/to/ace/ace.conf)
          --copy_from <file>    : Retrieves file from all hosts in group
          --copy_to <file>      : Copy operation (Multiple)
          --destination <dir>   : Set destination for copied files
          --exec "cmd"          : Execute cmd (Multiple)
          --group group{,x,y}   : Specify groups for operation, on all specified groups
          --group group{+x+y}   : Specify groups for operation, only on hosts in ALL specified groups
          --help                : Display the program help
          --identity <file>     : Use specified identity file to connect
          --list                : Show list of groups in the configuration file
          --log                 : Write the output of all commands to /tmp/ace-(time)_(date).log
          --password            : Specify to use a password (will be prompted for it)
          --username <user>     : Connect as user
          --version             : Display verion of ace

        Configuration file Syntax
          Notes:
            1. All lines beginning with "#" are ignored.
            2. Any text after a "#" on a single line are ignored.

        Each line within the configuration file is for a single
        host, and formatted as follows.

      [HOSTNAME]:[GROUP]{,GROUP,GROUP,...}

      --------------------------------------------------------------

