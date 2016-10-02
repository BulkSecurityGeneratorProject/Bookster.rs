# Bookster.rs Official Repository


## Arhitecture overview
~~~
                                                   /-------------\
                                                   |   Browser   |
                                                   \------+------/
                                                          |
                                                          |
                                                          V 8080
                               /-----------------------------------------------------\
                               | Gateway                                             |
                               | +-----------+    +--------------+      +----------+ |
                               | |           |    |  Zuul Proxy  |      |          | |     +-------+
                               | | Angular   |    |              |      |  Access  +-|---->|       |
                               | | App       |    +--------------+      |  Control | |     | Users |
                               | |           |    |    Ribbon    |      |          | |     | Roles |
                               | +-----------+    +---+------+---+      +----------+ |     +-------+
                               |                      |      |                       |
                               \-+---------------------------------------------------/
                                 |                    |      |       
                                 |                    |      |                              
                                 |                    |      |                        
                                 |        +-----------/      \----------------+            
/-----------------------\        |        |                                   |
| JHipster Registry     |        |        V 8081                              V 8082
|                       |        | /-------------\     +-----+         /-------------\     +-----+
|  +-----------------+  |        | |             |     |     |         |             |     |     |
|  | Eureka Server   |  |        | |  Book Service +-->| DB1 |         |  Service 2  +---->| DB2 |
|  +-----------------+  |        | |             |     |     |         |             |     |     |
|  | Config Server   |  |        | \--+-----+----/     +-----+         +--+------+---/     +-----+
|  +--------+--------+  |  8761  |    |     |                             |      |
|           |           |<-------+----+-----------------------------------/      |
\-----------------------/                   |                                    |
            |                               \-------------+----------------------/
            V                                             |
        +-------+                                         |
        |       |                 /------------------------------------------------\
        |  Git  |                 | ELK                   |                        | 
        |  Repo |                 |                       V 5000                   |
        +-------+                 | +---------+      +----------+      +--------+  |
                                  | | Elastic |      | Logstash |      | Kibana |  |
                                  | | Search  |<-----|          |      |        |  |
                                  | +---------+      +----------+      +--------+  |
                                  \------------------------------------------------/
~~~


## Development

Before you can build this project, you must install and configure the following dependencies on your machine:

1. [Node.js][]: We use Node to run a development web server and build the project.
   Depending on your system, you can install Node either from source or as a pre-packaged bundle.

After installing Node, you should be able to run the following command to install development tools (like
[Bower][] and [BrowserSync][]). You will only need to run this command when dependencies change in package.json.

    npm install

We use [Gulp][] as our build system. Install the Gulp command-line tool globally with:

    npm install -g gulp

Run the following commands in two separate terminals to create a blissful development experience where your browser
auto-refreshes when files change on your hard drive.

    ./mvnw
    gulp

Bower is used to manage CSS and JavaScript dependencies used in this application. You can upgrade dependencies by
specifying a newer version in `bower.json`. You can also run `bower update` and `bower install` to manage dependencies.
Add the `-h` flag on any command to see how you can use it. For example, `bower update -h`.


## Building applications for production

    ./mvnw -Pprod clean package

## Testing

Unit tests are run by [Karma][] and written with [Jasmine][]. They're located in `src/test/javascript/` and can be run with:

    gulp test