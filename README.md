C5
====================
[![Build status](https://travis-ci.org/OhmData/c5.svg)](https://travis-ci.org/OhmData/c5) [![HuBoard badge](http://img.shields.io/badge/Hu-Board-7965cc.svg)](https://huboard.com/OhmData/c5)

C5 is a simple, scalable, open source distributed database that is compatible with the HBase client API. Your code
that talks to HTable and/or HBaseAdmin can talk to the C5 client too.

Like HBase, C5 is a BigTable-flavoured ACID database. Internally, C5 uses the same HFile format that HBase uses for storing data.

Building and running
--------------------
To build this project, simply

    mvn install

(optionally followed with `-DskipTests=true`) to build the C5 daemons and client libraries (and optionally skip the tests).

To start the C5 server in single-node mode,

    cd c5db/
    ./bin/run_test_server.sh

after building the project. One can think of the run_test_server script as an example of how to start the server.

-D options of C5 include

- `regionServerPort=<port #>`
- `webServerPort=<port #>`
- `clusterName=<The name of the cluster>`
- `org.slf4j.simpleLogger.defaultLogLevel=<log level>`
- `org.slf4j.simpleLogger.log.org.eclipse.jetty=<log level>`

These options apply when running the server's main class, c5db.Main, as the run_test_server script illustrates.

Examples
--------
Examples of how to access the server can be found in the tests in project module __c5-end-to-end-tests__. In
addition, a web status console will start on port 31337. Information about the cluster while it's running can be found there:
just navigate to http://localhost:31337 in your browser.

Replication/consensus API
---------------
C5 makes use of an implementation of the Raft consensus protocol to replicate its write-ahead log; this implementation may
also be used independently of C5 to replicate arbitrary data. For the API, see the project module __c5-api__. Also see modules
__c5db-replicator__ and __c5db-olog__ for the Raft implementation itself. Example usage may be found in the tests in project
module __c5-general-replication__.

Log-reading utility
-------------------

Also provided is a standalone utility for reading the logs generated by C5's Raft; the code for this utility is in module __c5db-cat-olog__,
and it may be run from the command line as:

    c5db-cat-olog/bin/cat_olog.sh <log file name>

Troubleshooting
---------------
On Mac OSX:

    export JAVA_HOME=`/usr/libexec/java_home -v 1.8`

More documentation
------------------
For more information about C5's code and package structure, please see the package-info.java files in project module __c5db__,
located in each package within that module. In addition, see the package-info.java file in the __c5db-replicator__ module in package c5db.replication;
and in the __c5db-olog__ module in package c5db.log, respectively.

C5 is hosted on GitHub at https://github.com/OhmData/c5.

