<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=utf-8">
    <title>dzlad - README</title>
</head>
<body style="background:#eeeeec;width:86%;margin-left:7%">
Dzlad functions as a command line interface to the [AUR][1]. It is written in Ruby.
  [1]: http://aur.archlinux.org "ArchLinux User Repository"

---

### Dependencies

  * ruby (1.9)
  * pacman (for -u)
  * tar (for -d)

---

### Usage

#### Download build scripts (PKGBUILD, INSTALL, etc.)

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em"><code>$ dzlad ffcast
<span style="color:#9AE25A;font-weight:bold">::</span> AUR package <span style="color:#FEF3B5;font-weight:bold">ffcast</span> saved in /tmp/aur/
$ cd ffcast
$ vim PKGBUILD
$ makepkg -csir
... ...
</code></pre>

#### Search for packages with a keyword

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em;font-weight:bold"><code><span style="font-weight:normal">$ dzlad -s firefox%pgo</span>
<span style="color:#E25AC5">aur</span>/<span style="color:#FEF3B5">firefox-pgo</span> <span style="color:#E25A6B">3.6-1</span> <span style="color:#4F3D53">|194|</span>
    <span style="font-weight:normal">Mozilla Firefox customizable web browser (XULRunner independent, PGO optimized, 64-bit TraceMonkey)</span>
<span style="color:#E25AC5">aur</span>/<span style="color:#FEF3B5">firefox-pgo-beta</span> <span style="color:#E25A6B">3.6-1</span> <span style="color:#4F3D53">|142|</span>
    <span style="font-weight:normal">Mozilla Firefox customizable web browser (XULRunner independent, PGO optimized, 64-bit TraceMonkey, beta)</span>
<span style="color:#E25AC5">aur</span>/<span style="color:#FEF3B5">firefox-pgo-minefield</span> <span style="color:#9AE25A">100207-1</span> <span style="color:#4F3D53">|9|</span>
    <span style="font-weight:normal">Mozilla Firefox customizable web browser (XULRunner independent, PGO optimized, 64-bit TraceMonkey, dev tree)</span>
<span style="color:#E25AC5">aur</span>/<span style="color:#FEF3B5">firefox-pgo-minefield-smp</span> <span style="color:#E25A6B">100204-1</span> <span style="color:#4F3D53">|14|</span>
    <span style="font-weight:normal">Mozilla Firefox customizable web browser (XULRunner independent, PGO optimized, 64-bit TraceMonkey, dev tree, multithreaded)</span>
</code></pre>

Note the *red* color of the version number indicates the package has been flagged out of date.
Also note that the AUR currently supports only two simple "regexp", i.e. *%* for any string and *_* for one arbitrary character.

#### Check for available upgrades for installed AUR packages

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em;font-weight:bold"><code><span style="font-weight:normal">$ dzlad -u</span>
<span style="background-color:#FEF3B5;color:#232527">firefox-pgo</span><span style="font-weight:normal">.......................</span><span style="color:#e2d65a">3.6.2-1 >> </span><span style="color:#E25A6B">3.6-1</span>
<span style="background-color:#FEF3B5;color:#232527">mypaint-git</span><span style="font-weight:normal">.......................</span><span style="color:#e2d65a">20100307-1 >> 20100208-2</span>
<span style="color:#FEF3B5">vim-snipmate</span><span style="font-weight:normal">......................</span><span style="color:#9AE25A">0.83-1 -> 0.83-5</span>
<span style="color:#9AE25A;font-weight:bold">::</span> <span style="font-weight:normal">Upgradable AUR Packages:
vim-snipmate</span>
</code></pre>

#### Upload .src.tar.gz to AUR

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em"><code>$ makepkg --source
... ...
$ dzlad -p msort-8.53-1.src.tar.gz@system:"New Release." --vote -u userfoo:passbar
<span style="color:#9AE25A;font-weight:bold">::</span> Uploaded msort-8.53-1.src.tar.gz [33319]
<span style="color:#9AE25A;font-weight:bold">::</span> Your votes have been cast for the selected packages.
</code></pre>

#### Vote, flag, notify, adopt, disown, delete, unvote, unflag, unnotify

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em"><code>$ dzlad -a delete -u userfoo:passbar -c -- yajl-ruby
<span style="color:#9AE25A;font-weight:bold">::</span> None of the selected packages could be deleted.
</code></pre>

Oops, \`delete' is TU/dev only ^

#### Also try...

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em"><code>$ dzlad -i dzlad
$ dzlad -m lolilolicon
$ dzlad --examples
</code></pre>

#### Use the dzlad ruby module in irb

<pre style="background-color:#232527;color:#6c6c6c;padding:0.8em 0.8em 0.8em 0.8em"><code>irb(main):001:0> require 'dzlad/aur'
=> true
irb(main):002:0> aur = Dzlad::AUR.new
=> #&lt;Dzlad::AUR user= login=false&gt;
irb(main):003:0> aur.login('userfoo', 'passbar')
=> "AURSID=N9N6576O77P75NPQRPS9899768Q58O79; path=/"
irb(main):004:0> aur.addComment('33877', "Please note the dzlad-git package has been removed.\n--This is a test.")
=> #&lt;Net::HTTPOK 200 OK readbody=true&gt;
</code></pre>

---

### Files

~/.dzlad/{cookie,upgrade\_ignore}
</body>
</html>
