apiarista
=========

Version `0.0.1` *unstable*.

*See also [apiarista-template](http://github.com/drojas/apiarista-template/).*

`apiarista` is a CLI tool to use along with [Node.js](http://nodejs.org/) and [Express](http://expressjs.com/).

It purpose is to take an [app template](http://github.com/drojas/apiarista-template/) and use it as a source for API structure and API resources generation.

###Installation

  $ npm install -g drojas/apiarista

###Usage

`$ apiarista` asumes an [Express](http://expressjs.com/) app

  $ npm install -g express
  $ express /tmp/foo && cd /tmp/foo
  $ npm install

Now you can use `apiarista` to plug a generic API to your project

    $ apiarista -h

     Usage: apiarista [options]

     Options:

       -h, --help                   output usage information
       -V, --version                output the version number
       -i, install                  install base api only
       -r, resource [ResourceName]  generate resource (default: "resource")
       -o, --owner [OwnerName]      define an owner (default: "user")
       -a, --auth                   authenticate the resource
       -t, --timestamp              add timestamp field to resource
       -f, --force                  disable abort on path exists
       -d, --debug                  output debug data

     Example:

       $ apiarista resource consumer --auth --timestamp
       $ apiarista -r user -a --owner consumer -t
       $ apiarista -r blog "title: { String, required: true }" -o user -t

### Example

    $ apiarista resource Poll "title: String" "ballots: []" -o -t

The flags `-o` and `-t` will add a owner (`ref: 'User'`) and a timestamp (`Date.now) to the resource Schema.

So, the following generates the same Schema:

    $ apiarista -r Poll "title: String" "ballots: []" "user: { type: Schema.ObjectId, ref: 'User' }"
    "date: { type: Date, default: Date.now }"

**IMPORTANT** `$ apiarista` also uses the `-o` flag to add ownership verification middleware to PUT and DELETE operations.

I recommend to use the `-o` and `-t` flags when a resource need to be owned and timestamped.

### Dependencies

[apiarista-template](http://github.com/drojas/apiarista-template/) depends on [Express](http://expressjs.com/) `v3.1.0`, [Mongoose](http://mongoosejs.com/) `v3.5.7` and [token.js](http://github.com/flesch/token.js/) `v0.0.1`.

`$ apiarista` will add that dependencies to your `package.json` if not present so after the generation process you probably should do. If your project depends on an older version of that packages no upgrade will be made.

    $ npm install

### Finally

    $ echo -e "\nrequire('./api')(app);" >> app.js
    $ node app.js

### Start consuming the API

    $ curl -X POST "http://127.0.0.1:3000/consumers"

------------

<pre>
     ^^      .-=-=-=-.  ^^
 ^^        (`-=-=-=-=-`)         ^^
         (`-=-=-=-=-=-=-`)  ^^         ^^
   ^^   (`-=-=-=-=-=-=-=-`)   ^^                            ^^
       ( `-=-=-=-(@)-=-=-` )      ^^
       (`-=-=-=-=-=-=-=-=-`)  ^^
       (`-=-=-=-=-=-=-=-=-`)              ^^
       (`-=-=-=-=-=-=-=-=-`)                      ^^
       (`-=-=-=-=-=-=-=-=-`)  ^^
        (`-=-=-=-=-=-=-=-`)          ^^
         (`-=-=-=-=-=-=-`)  ^^                 ^^
     jgs   (`-=-=-=-=-`)
            `-=-=-=-=-`
</pre>