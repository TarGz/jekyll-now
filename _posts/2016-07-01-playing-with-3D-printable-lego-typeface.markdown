---
layout: post
title:  "Playing with 3D printable Lego typeface"
date: 	Jun 20th, 2016 12:00:00am
categories: leisure
comments: true
preview: "images/leisure/brickolage/brickfont/01.jpg"
excerpt: "Writting with Lego have been something I've been interested for a while, my 3D printer push me to go further"
---
![Lego wall](/images/leisure/brickolage/brickfont/02.jpg)

I have been fan of Lego and pixel art since my childwood so I decided to create a Lego wall in my DigitasLBi Labs office. Then we started making pixel art using small bricks. I set this wall as an open canvas where everybody could create, I started with Mario Bross and then Bomberman appear with bob the sponge, space invaders, etc. And yes I also made a Lego Qr-Code :-)... Later people used the wall to display messages or font based logo. Design text message using Lego is quite chanlenging and you often end up with a deceptive result. That's where the idea of creating some "Lego" brick fontface came.

![Lego wall](/images/leisure/brickolage/02.jpg)


### THE FIRST POC

I started designing "Lego" chars by hand using 123Design but that rapidly became a nigthmare because a Lego brick is quite complexe. I also wanted to be abble to generate all font char at once. But a least I had a first working POC:


<div class="uk-grid" data-uk-grid-margin="">
    <div class="uk-width-large-1-3 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/square04.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-3 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/square05.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-3 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/square06.jpg" class="uk-responsive-width">
    </div>
</div>


### SEEKING FOR THE RIGHT TOOL

After exploring different 3D software and CAD tools I finally discovered an opensource 3D CAD software named [OpenScad](http://www.openscad.org/). That was exactly what I was looking for, it's a programing language capable of generating 3D model using simple [3D shape and boolean operation](http://www.openscad.org/cheatsheet/). You can easely create whatever you want. You can also use a lot of differents [library](https://github.com/openscad/openscad/wiki/Libraries) developped by the community. The amazing part of this tools is his ability to generate 3D model dynamicaly. For my needs I have create a script capable  of generating all the parts of a brick. After that it looks like this to generate A,B and C chars:

{% highlight javascript%}
renderBrick() Letter("A");
renderBrick() Letter("B");
renderBrick() Letter("C");
{% endhighlight %}

That's usefull but you still need some manual work to generate the full set of chars of the font. An other great part of [OpenScad](http://www.openscad.org/) is his [CLI ability](https://en.wikibooks.org/wiki/OpenSCAD_User_Manual/Using_OpenSCAD_in_a_command_line_environment). Using Bash script you can call your [OpenScad](http://www.openscad.org/) script with a set of parameters in my case I was abble to pass a list of chars and a font ID to generate all chars from a font.

{% highlight bash%}
string=${2}
array=(${string//,/ })
for i in "${!array[@]}"
do
  echo -e "generating: \033[35m"${array[i]}"\033[0m"
  openscad -o output/${3}-${fontArray[${3}]}/CHAR/${array[i]}.stl -D debug_mode=false -D fontID=${3}  -D 'letter="'${array[i]}'"' bricks_gen.scad
{% endhighlight %}

> I now have a fully configurable bash script capable of generating a full set of chars

![Brickolage](/images/leisure/brickolage/09.jpg)

### USING EXISTING FONT-FACE

Using any existing font is a great source of creativity, thanks to my OpenScad script I was abble to generate any font but I wanted to generate bricks that fit prefectly with Lego sizes and constraints. Chars width & heigth need to be proportional to the lego knobs spacing. That's where I starded design two font face ["Brick font"](#x5-font-named-brickfont) and ["Brickolage"](#x8-font-brickolage).

#### *Long Shot*
<div class="uk-grid" data-uk-grid-margin="">
    <div class="uk-width-large-1-1 uk-width-medium-1-1 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/long-shot/01.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/long-shot/02.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/long-shot/03.jpg" class="uk-responsive-width">
    </div>
</div>


#### *Phosphate*
<div class="uk-grid" data-uk-grid-margin="">
    <div class="uk-width-large-1-1 uk-width-medium-1-1 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/Phosphate/01.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/Phosphate/02.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/Phosphate/04.jpg" class="uk-responsive-width">
    </div>
</div>


#### *Birds of paradise*
<div class="uk-grid" data-uk-grid-margin="">
    <div class="uk-width-large-1-1 uk-width-medium-1-1 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/birds-of-paradise/01.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/birds-of-paradise/02.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/birds-of-paradise/03.jpg" class="uk-responsive-width">
    </div>
</div>




### CREATING A "LEGO" FONT-FACE

#### *3X5 FONT NAMED BRICKFONT*


<div class="uk-grid" data-uk-grid-margin="" id="BRICKFONT">
    <div class="uk-width-large-1-1 uk-width-medium-1-1 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/brickfont/01.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/brickfont/02.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/brickfont/04.jpg" class="uk-responsive-width">
    </div>

</div>

#### *4X8 FONT BRICKOLAGE*

<div class="uk-grid" data-uk-grid-margin="" id="BRICKOLAGE">
    <div class="uk-width-large-1-1 uk-width-medium-1-1 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/brickolage/01.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/brickolage/02.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <img src="/images/leisure/brickolage/brickolage/04.jpg" class="uk-responsive-width">
    </div>
</div>




### 3D PRINTING CHALENGES

![Brickolage](/images/leisure/brickolage/17.jpg)

Once designed and generated chars have to be printed. This pieces seamms easy to printed at the first tougth but I faced a lot of issues with bridging and overall quality. After a lot of different seettings and software I finaly been abble to print acceptable quality using [Simplify 3D](https://www.simplify3d.com/).

<div class="uk-grid">
    <div class="uk-width-large-1-2 uk-width-medium-1-1 uk-width-small-1-1">
        <iframe src="https://vine.co/v/eiz3rQT6i1A/embed/simple" width="550" height="550" frameborder="0" class="uk-responsive-width"></iframe>
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-1 uk-width-small-1-1">
        <iframe src="https://vine.co/v/eKElLt3q00U/embed/simple" width="550" height="550" frameborder="0" class="uk-responsive-width"></iframe>
    </div>
</div>


### CREATIONS

This technic of generating brick from font inspired me to create some motivationnal posters, doors sign for my kids and message for the office.

<div class="uk-grid" data-uk-grid-margin="">
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <blockquote>La vie est belle</blockquote>
        <img src="/images/leisure/brickolage/square03.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <blockquote>La vie est belle</blockquote>
        <img src="/images/leisure/brickolage/square07.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <blockquote>Non smoking area</blockquote>
        <img src="/images/leisure/brickolage/square08.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <blockquote>All you need is...</blockquote>
        <img src="/images/leisure/brickolage/square02.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <blockquote>Kids door sign</blockquote>
        <img src="/images/leisure/brickolage/square09.jpg" class="uk-responsive-width">
    </div>
    <div class="uk-width-large-1-2 uk-width-medium-1-2 uk-width-small-1-1">
        <blockquote>All you need is love</blockquote>
        <img src="/images/leisure/brickolage/square10.jpg" class="uk-responsive-width">
    </div>
</div>

> Stay young and play Lego derivated from my [Stay Young poster](/project/stay-young-and-play-lego/).

![Brickolage](/images/leisure/brickolage/vertical01.jpg)

I'm still exploring what to do with this, any ideas or maybe you want a custom font or a door sign ? feel free to ask.











