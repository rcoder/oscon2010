!SLIDE title-slide

# Don't Fear the Closure #

## Lennon Day-Reynolds ##
## Dark Horse Comics ##
## [lennond@darkhorse.com](mailto:lennond@darkhorse.com) :: [http://rcoder.net/](http://rcoder.net/) ##


!SLIDE bullets incremental

# History #

* Created as LiveScript by Brendan Eich in 1995
* Renamed + recast in a supporting role for Java


!SLIDE bullets incremental

# History, cont. #

* MS won an effective browser monopoly
* JS stagnated while they built C# and the CLR
* ...and then, Oddpost + GMail made it important again


!SLIDE bullets incremental

# What is JavaScript? #

* Objects
* Functions
* Core types: Object, Array, RegExp, Date, etc.


!SLIDE bullets incremental

# JavaScript.prototype = Scheme

* Clean, research-oriented dialect of Lisp
* Functions are first-class values
* Structure programs by passing _continuation_ functions


!SLIDE 

# Scheme example

    (define (adder i)
        (lambda (x) (+ x i)))


!SLIDE

# ...in Javascript

    @@@JavaScript
    var adder = function(i) {
        return function(x) { return x + i; }
    };


!SLIDE bullets incremental

# JavaScript Objects #

* Namespace
* Prototype
* "Open" by default


!SLIDE bullets incremental

# JavaScript.prototype = Self

* Released in 1990
* Objects have slots
* Slots may be data, methods, or parents
* All interaction is via message-passing


!SLIDE bullets incremental

# Self, cont. #

* Designed for long-lived objects
* No fixed classes, so objects can evolve
* Any number of parent slots can be searched for missing slots
* Traits and prototypes are special cases of parents


!SLIDE

# Self example #

<p style="text-align:center">
    <img src="/bank2.gif"/><br/><br/>
    <small>(Image copyright &copy; Oracle Corp.)</small>
</p>


!SLIDE bullets incremental

# Prototypes in JavaScript #

* Is-a vs. has-a
* JavaScript objects have at most one prototype
* DOM nodes inherit properties from containers


!SLIDE

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


!SLIDE bullets incremental

# A personal confession #

* I _hated_ Javascript for many years


!SLIDE

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


!SLIDE

# How I got better


!SLIDE

# Closures #

    @@@ JavaScript
    function Counter() {
        var value = 0;

        this.incr = function() {
            value += 1;
        }

        this.getValue() {
            return value;
        }
    }


!SLIDE

# How I got better, cont. #

    @@@ JavaScript
    // Yay for jQuery!
    $(".required-field").blur(function() {
        var me = $(this);
        var value = me.val();
        if (!value) {
            me.append("<em>* required</em>");
        }
    });


!SLIDE bullets incremental

# Why jQuery rocks #

* Finally, a standard library for JavaScript
* Uses Self-like slots with getters/setters
* Bind simple callback functions, rather than classes


!SLIDE bullets incremental

# jQuery weaknesses #

* Still needs data-modeling support
* Also bound to browser concurrency (or lack thereof)


!SLIDE bullets incremental

# JavaScript.next() #

* Concurrency
* Better Syntax


!SLIDE bullets incremental

# JavaScript concurrency: Web Workers #

* Concurrent, sandboxed processes
* Pass messages to and from calling page
* Unable to access the DOM, network, or filesystem


!SLIDE bullets incremental

# Web Workers, cont. #

* Function like processes from Erlang (but heavy-weight!)
* No shared state, so you can't deadlock
* Available in Firefox, Safari, Chromium/Chrome, Opera


!SLIDE

# Web Workers example #

    @@@ JavaScript
    var worker = new WebWorker('doubler.js');

    worker.onMessage = function (event) {
        console.log(event.data.toString());
    }

    worker.postMessage("2");


!SLIDE

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


!SLIDE 

# New syntax: 'let' #

!SLIDE bullets incremental

# 'let' expressions

* Binds variables within the current _block_
* Protects variables with the same name in outer blocks
* Like 'letrec' in Scheme, 'my' in Perl
* Available in JS 1.7 (i.e., only Firefox)


!SLIDE

    @@@ JavaScript
    var x = 5;

    if (true) {
        let x = 6;
        console.log(x); // => prints "6"
    }

    console.log(x); // => prints "5"


!SLIDE bullets incremental

# New syntax: Destructuring #

* Called 'pattern matching' in Haskell, ML
* Limited form (array/list unpacking) also in P* languages

!SLIDE

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


!SLIDE bullets incremental

# New syntax: miscellany

* Generators, iterators
* 'const' bindings
* Modules
* ...very little of it coming all that soon :(


!SLIDE bullets incremental

# Conclusions

* JavaScript is actuall a cool language
* Sadly, shackled to weak/inconsistent runtime 
* Libraries are helping, but the language needs to evolve
* Learning weird research langauges will help your JS coding

