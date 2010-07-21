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

* finally, a standard library for JavaScript
* handles views pretty well
* still needs data-modeling support

