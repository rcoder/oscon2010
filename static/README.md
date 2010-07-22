
# Don't Fear the Closure #

## Lennon Day-Reynolds ##
## Dark Horse Comics ##
## @rcoder :: http://rcoder.net/



# Goals #

* Language history
* Useful patterns
* Hope



# JavaScript History #

* Created as LiveScript by Brendan Eich in 1995
* Renamed + recast in a supporting role for Java
* Used to build roll-overs, animated text, other annoyances



# History, cont. #

* IE won an effective browser monopoly
* JS stagnated while MS built C# and the CLR
* ...and then, Oddpost + GMail made it important again



# What is JavaScript? #

* Functions
* Objects
* Core types: Object, Array, RegExp, Date, etc.



# JavaScript functions #

* Executable code
* Lexical environment
* First-class objects



# Function.prototype = Scheme

* Built at MIT 1975-80, standardized in RnRS specs
* Clean, research-oriented dialect of Lisp
* Functions are first-class values
* Programs operate on themselves



# Scheme example

    (define (make-greeter msg)
        (lambda (s) 
            (string-append msg s)))

    (define yo-greeter (make-greeter "Yo "))


# ...in Javascript

    @@@JavaScript
    var makeGreeter = function(msg) {
        return function(s) {
            return msg + s;
        }
    }

    var yoGreeter = makeGreeter("Yo ");



# Other similarities #

* Weak standard library
* Many (incompatible) implementations
* Considered a "toy language" by many programmers



# JavaScript Objects #

* Namespace
* Attributes
* Prototype



# Object.prototype = Self

* Built at PARC, released by Sun in 1990 
* Objects have slots
* Slots contain data or methods
* _All_ interaction is via message-passing



# Self, cont. #

* Designed for long-lived objects
* No fixed classes, so objects can evolve
* Any number of parent slots can be searched for missing slots
* Traits and prototypes are special cases of parents



# Self example #

<p style="text-align:center">
    <img src="bank12.gif"/><br/><br/>
    <small>(Image copyright &copy; Oracle Corp.)</small>
</p>



# Prototypes in JavaScript #

* JavaScript objects have at most one prototype
* DOM nodes inherit properties from containers
* "is-a" vs. "is-in"



# Useful prototypes in JavaScript

    @@@ JavaScript
    function Resource(url) {
        this.url = url;
        this.ready = false;
        this.data = {};
    }

    Resource.prototype.get = function(func) {
        this.ready = false;
        $.get(this.url, function(data) {
            this.data = data;
            this.ready = true;
            if (func) { func(this); }
        }, 'json');
    }



# A personal confession #

* I _hated_ Javascript for many years



# Why I hated JavaScript #

    @@@ HTML
    <!-- mixing markup and code -->
    <input name="first_name" type="text" 
        onchange="return 
            checkField(this,'required field')"/>

    <script>
        // globals, globals, everywhere
        globalElem = 
            document.getElementById('#an-elem');

        processGlobalElem();
    </script>



# How I got better

* Write JavaScript like its weird parents



# Read these books #

<p style="text-align: center;">
    <img src="javascript.gif"/>
    <img src="jquery.jpg"/>
</p>



# Ruthlessly cull bad code

* <s>eval</s>
* <s>with</s>
* <s>globals</s>



# Use more closures #

    @@@ JavaScript
    function Counter() {
        var value = 0;

        this.incr = function() {
            value += 1;
        }

        this.getValue() {
            return value;
        }

        return this;
    }



# Use jQuery #

    @@@ JavaScript
    $(".required-field").blur(function() {
        var me = $(this);
        var value = me.val();
        if (!value) {
            me.append("<em>* required</em>");
        }
    });



# Why jQuery rocks #

* Finally, a standard library for JavaScript
* Encourages good habits
* Uses Self-like slots with getters/setters
* Bind simple callback functions, rather than classes



# jQuery weaknesses #

* Still needs data-modeling support
* Also bound to browser concurrency (or lack thereof)



# JavaScript.next() #

* Concurrency
* New Syntax



# JavaScript concurrency: Web Workers #

* Parallel, sandboxed processes
* Pass messages to and from calling page
* Unable to access the DOM, network, or filesystem



# Web Workers, cont. #

* Function like processes from Erlang (but heavy-weight!)
* No shared state, so you can't deadlock
* Available in Firefox, Safari, Chromium/Chrome, Opera



# Web Workers example #

    @@@ JavaScript
    var worker = new WebWorker('doubler.js');

    worker.onMessage = function (event) {
        console.log(event.data.toString());
    }

    worker.postMessage("2");



# Web Workers example, cont. #
    @@@ JavaScript
    // doubler.js
    onMessage = function(event) {
        var data = event.data;

        if (data) {
            var number = Number(data);
            postMessage(number * 2);
        }
    }



# New syntax: 'let' #


# 'let' expressions

* Binds variables within the current _block_
* Protects variables with the same name in outer blocks
* Like 'letrec' in Scheme, 'my' in Perl
* Available in JS 1.7 (i.e., only Firefox)



    @@@ JavaScript
    var x = 5;

    if (true) {
        let x = 6;
        console.log(x); // => prints "6"
    }

    console.log(x); // => prints "5"



# New syntax: Destructuring #

* Called 'pattern matching' in Haskell, ML
* Limited form (array/list unpacking) also in P* languages


# Destructuring, cont. #

    @@@ JavaScript
    // array destructuring
    var (a, b, c) = [1, 2, 3];

    // object destructuring
    var obj = {
        name: "an object",
        size: [10, 10]
    };

    var {name, size} = obj;



# New syntax: miscellany

* Generators, iterators
* 'const' bindings
* Modules
* ...very little of it coming all that soon :(



# Conclusions

* JavaScript is actually a cool language
* Sadly, shackled to weak/inconsistent runtime 
* Libraries are helping, but the language needs to evolve
* Learning weird research langauges will help your JS coding

