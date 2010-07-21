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

![Self source](http://labs.oracle.com/self/release_4.0/Self-4.0/Tutorial/Images/Bank/bank2.gif)


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

# JavaScript.prototype = Lisp

* Functions are first-class values
* Structure programs by passing _continuation_ functions


!SLIDE bullets incremental

# A personal confession #

* I _hated_ Javascript for many years


!SLIDE

# Why I hated JavaScript #

    @@@ HTML
    <input name="first_name" type="text" 
        onchange="return 
            checkField(this,'required field')"/>

    <a href="javascript:
        displayAnnoyingDialog('hello!')"/>


!SLIDE

# jQuery #

    @@@ JavaScript
    $(".required-field").blur(function() {
        var value = $(this).val();
        if (!value) {
            $(this).append("<span 
                class='req-msg'>
                    * required field
                </span>");
            }
        }
    });


!SLIDE bullets incremental

# jQuery, cont. #

* Finally, a standard library for JavaScript
* Handles views pretty well
* Still needs data-modeling support
* Also bound to browser (lack of) concurrency


!SLIDE bullets incremental

# JS.now #

* Web Workers
* New storage tools (offline cache, localStorage)
* Display widgets (A/V, canvas)


!SLIDE bullets incremental

# Web Workers #

* Concurrent, sandboxed processes
* Pass messages to and from calling page
* Unable to access the DOM, network, or filesystem


!SLIDE bullets incremental

# Web Workers, cont. #

* Function like actors/processes from Erlang
* No shared state, so you can't deadlock
* Issues with payload formats across browsers


!SLIDE

# Trivial actor-based service #

    @@@ Erlang
    -module(doubler).
    -export([spawn_worker/0, double/1]).

    double() -> 
        receive
            Val -> Val * 2;
        end.

    spawn_worker() -> 
        Pid = spawn(?MODULE, double, []).
        Pid.


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


!SLIDE bullets incremental

# JS.future #

* Destructuring
* let bindings
