# ship-it

[![GitLab CI Status](https://gitlab.com/ship-it/ship-it/badges/master/build.svg)](https://gitlab.com/ship-it/ship-it) [![AppVeyor CI Status](https://ci.appveyor.com/api/projects/status/7k9emo9byxy8y8wk/branch/master?svg=true)](https://ci.appveyor.com/project/ChristianWitts/ship-it/branch/master)


A log shipper similar to logstash and fluentd, written in Rust, initially as a learning
exercise for myself, and then adding a tranche of features as time goes on and I get 
more familiar with the language, and the tooling I want to plug it into.

* `tail -f` type functionality
* Multi-file support
* Configuration for what to watch, and how to parse it
* Support for tcp/udp sockets for applications to stream to
* Shipping logs to a 'server' for processing and aggregation

The idea would be to build something that will read and structure logs,
which are then sent to a streaming server (probably Wallaroo), for it to be
processed down to something consuming less storage on disk to be read back
at a later stage.

For the concept of just web-server type logs, the happy path could be distilled
down to a small structure possibly as such:

* Hostname => 2 bytes
* Endpoint => 1 byte
* Source IP => 4 bytes
* Response time => 1 byte?
* Status Code => 1 byte
* Timestamp => 4 bytes
* UA String => 2 bytes

such that we can decompose a ~120 byte log entry down to ~15 bytes, yielding a 
decent saving on storage.

