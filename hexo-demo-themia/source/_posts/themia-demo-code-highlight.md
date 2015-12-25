title: "Highlighted Code"
date: 2015-09-08 20:02:11
layout: 
link: 
categories:
 - Themia
tags: 
 - themia 
 - hexo
 - code
 - highlight

clearReading: false
metaAlignment: left
thumbnailImage: http://7xih5c.com1.z0.glb.clouddn.com/15-10-7/7722088.jpg
coverImage: 
coverSize: 
coverCaption: 
coverMeta: 
photos:

comments: true

---
展示在日志中插入代码块，支持高亮显示，并且有几种显示代码块的模式，能显示本地或者远程托管的代码。
支持多语言代码检测以及高亮。
<!-- more -->

<!-- toc -->

## 基础使用
### Normal code block

```
alert('Hello World!');
```

### With caption

{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}

### With caption and URL

{% codeblock .compact http://underscorejs.org/#compact Underscore.js %}
.compact([0, 1, false, 2, ‘’, 3]);
=> [1, 2, 3]
{% endcodeblock %}

### Gist

{% gist 996818 %}

### jsFiddle

{% jsfiddle ccWP7 %}



## 多语言高亮支持

### APACHECONF
{% codeblock apache.conf https://github.com/kaedea GitHub %}
# rewrite`s rules for wordpress pretty url
LoadModule rewrite_module  modules/mod_rewrite.so
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php [NC,L]

ExpiresActive On
ExpiresByType application/x-javascript  "access plus 1 days"

Order Deny,Allow
Allow from All

<Location /maps/>
  RewriteMap map txt:map.txt
  RewriteMap lower int:tolower
  RewriteCond %{REQUEST_URI} ^/([^/.]+)\.html$ [NC]
  RewriteCond ${map:${lower:%1}|NOT_FOUND} !NOT_FOUND
  RewriteRule .? /index.php?q=${map:${lower:%1}} [NC,L]
</Location>
{% endcodeblock %}


### BASH
{% codeblock sample.bash https://github.com/kaedea GitHub %}
#!/bin/bash

###### BEGIN CONFIG
ACCEPTED_HOSTS="/root/.hag_accepted.conf"
BE_VERBOSE=false
###### END CONFIG

if [ "$UID" -ne 0 ]
then
 echo "Superuser rights is required"
 echo 'Printing the # sign'
 exit 2
fi

if test $# -eq 0
then
elif test [ $1 == 'start' ]
else
fi

genApacheConf(){
 if [[ "$2" = "www" ]]
 then
  full_domain=$1
 else
  full_domain=$2.$1
 fi
 host_root="${APACHE_HOME_DIR}$1/$2/$(title)"
 echo -e "# Host $1/$2 :"
}
{% endcodeblock %}


### Coffeescript
{% codeblock sample.coffee https://github.com/kaedea GitHub %}
###
Some tests
###
class Animal
  constructor: (@name) ->
  move: (meters) -> alert @name + " moved " + meters + "m."

class Snake extends Animal
  move: ->
    alert 'Slithering...'
    super 5

number   = 42; opposite = true


square = (x) -> x * x

range = [1..2]
list = [1...5]

math =
  root:   Math.sqrt
  cube:   (x) => x * square x

race = (winner, runners...) ->
  print winner, runners

alert "I knew it!" if elvis?

cubes = math.cube num for num in list

text = """
 Result
    is #{ @number }"""

html = '''   <body></body>'''

String::dasherize = ->
  this.replace /_/g, "-"
SINGERS = {Jagger: "Rock", Elvis: "Roll"}

t = ///
#{ something }[a-z]
///

$('.shopping_cart').bind 'click', (event) =>
    @customer.purchase @cart

hi = `function() {
  return [document.title, "Hello JavaScript"].join(": ");
}`
{% endcodeblock %}


### C++
{% codeblock sample.cpp https://github.com/kaedea GitHub %}
/*
 * Block comment
 */
#include <vector>

using namespace std;  // line comment
namespace foo {

  typedef struct Struct {
    int field;
  } Typedef;
  enum Enum {Foo = 1, Bar = 2};

  Typedef *globalVar;
  extern Typedef *externVar;

  template<typename T, int N>
  class Class {
    T n;
  public:
    void function(int paramName) {
      int *localVar = new int[1];
      this->n = N;

    label:
      printf("Formatted string %d\n\g", localVar[0]);
      printf(R"**(Formatted raw-string %d\n)**", 1);
      std::cout << (1 << 2) << std::endl;

    #define FOO(A) A
    #ifdef DEBUG
      printf("debug");
    #endif
    }
  };
}
{% endcodeblock %}


### C#
{% codeblock sample.cs https://github.com/kaedea GitHub %}
using System;

#pragma warning disable 414, 3021

public class Program
{
    /// <summary>The entry point to the program.</summary>
    public static int Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
        string s = @"This
""string""
spans
multiple
lines!";
        return 0;
    }
}

async Task<int> AccessTheWebAsync()
{
    // ...
    string urlContents = await getStringTask;
    return urlContents.Length;
}
{% endcodeblock %}


### CSS
{% codeblock sample.css https://github.com/kaedea GitHub %}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  body:first-of-type pre::after {
    content: 'highlight: ' attr(class);
  }
  body {
    background: linear-gradient(45deg, blue, red);
  }
}

@import url('print.css');
@page:right {
 margin: 1cm 2cm 1.3cm 4cm;
}

@font-face {
  font-family: Chunkfive; src: url('Chunkfive.otf');
}

div.text,
#content,
li[lang=ru] {
  font: Tahoma, Chunkfive, sans-serif;
  background: url('hatch.png') /* wtf? */;  color: #F0F0F0 !important;
  width: 100%;
}
{% endcodeblock %}


### DIFF
{% codeblock sample.diff https://github.com/kaedea GitHub %}
Index: languages/ini.js
===================================================================
--- languages/ini.js    (revision 199)
+++ languages/ini.js    (revision 200)
@@ -1,8 +1,7 @@
 hljs.LANGUAGES.ini =
 {
   case_insensitive: true,
-  defaultMode:
-  {
+  defaultMode: {
     contains: ['comment', 'title', 'setting'],
     illegal: '[^\\s]'
   },

*** /path/to/original timestamp
--- /path/to/new      timestamp
***************
*** 1,3 ****
--- 1,9 ----
+ This is an important
+ notice! It should
+ therefore be located at
+ the beginning of this
+ document!

! compress the size of the
! changes.

  It is important to spell
{% endcodeblock %}



### GO
{% codeblock sample.go https://github.com/kaedea GitHub %}
package main

import (
    "fmt"
    "os"
)

const (
    Sunday = iota
    numberOfDays  // this constant is not exported
)

type Foo interface {
    FooFunc(int, float32) (complex128, []int)
}

type Bar struct {
    os.File /* multi-line
               comment */
    PublicData chan int
}

func main() {
    ch := make(chan int)
    ch <- 1
    x, ok := <- ch
    ok = true
    float_var := 1.0e10
    defer fmt.Println('\'')
    defer fmt.Println(`exitting now\`)
    var fv1 float64 = 0.75
    go println(len("hello world!"))
    return
}
{% endcodeblock %}



### HTTP
{% codeblock sample.http https://github.com/kaedea GitHub %}
POST /task?id=1 HTTP/1.1
Host: example.org
Content-Type: application/json; charset=utf-8
Content-Length: 19

{"status": "ok", "extended": true}
{% endcodeblock %}

### INI
{% codeblock sample.ini https://github.com/kaedea GitHub %}
;Settings relating to the location and loading of the database
[Database]
ProfileDir=.
ShowProfileMgr=smart
Profile1_Name[] = "\|/_-=MegaDestoyer=-_\|/"
DefaultProfile=True
AutoCreate = no

[AutoExec]
use-prompt="prompt"
Glob=autoexec_*.ini
AskAboutIgnoredPlugins=0
{% endcodeblock %}

### Java
{% codeblock sample.java https://github.com/kaedea GitHub %}
/* Block comment */
import java.util.Date;
/**
 * Doc comment here for <code>SomeClass</code>
 * @see Math#sin(double)
 */
@Annotation (name=value)
public class SomeClass<T extends Runnable> { // some comment
  private T field = null;
  private double unusedField = 12345.67890;
  private UnknownType anotherString = "Another\nStrin\g";
  public static int staticField = 0;

  public SomeClass(AnInterface param, int[] reassignedParam) {
    int localVar = "IntelliJ"; // Error, incompatible types
    System.out.println(anotherString + toString() + localVar);
    long time = Date.parse("1.2.3"); // Method is deprecated
    int reassignedValue = this.staticField;
    reassignedValue ++;
    field.run();
    new SomeClass() {
      {
        int a = localVar;
      }
    };
    reassignedParam = new ArrayList<String>().toArray(new int[0]);
  }
}
enum AnEnum { CONST1, CONST2 }
interface AnInterface {
  int CONSTANT = 2;
  void method();
}
abstract class SomeAbstractClass {
}
{% endcodeblock %}

### JavaScript
{% codeblock sample.js https://github.com/kaedea GitHub %}
function $initHighlight(block, flags) {
  try {
    if (block.className.search(/\bno\-highlight\b/) != -1)
      return processBlock(block.function, true, 0x0F) + ' class=""';
  } catch (e) {
    /* handle exception */
    var e4x =
        <div>Example
            <p>1234</p></div>;
  }
  for (var i = 0 / 2; i < classes.length; i++) { // "0 / 2" should not be parsed as regexp
    if (checkCondition(classes[i]) === undefined)
      return /\d+[\s/]/g;
  }
  console.log(Array.every(classes, Boolean));
}
{% endcodeblock %}

### Json
{% codeblock sample.json https://github.com/kaedea GitHub %}
[
  {
    "title": "apples",
    "count": [12000, 20000],
    "description": {"text": "...", "sensitive": false}
  },
  {
    "title": "oranges",
    "count": [17500, null],
    "description": {"text": "...", "sensitive": false}
  }
]
{% endcodeblock %}

### MakeFile
{% codeblock sample.mak https://github.com/kaedea GitHub %}
# Makefile

BUILDDIR      = _build
EXTRAS       ?= $(BUILDDIR)/extras

.PHONY: main clean

main:
	@echo "Building main facility..."
	build_main $(BUILDDIR)

clean:
	rm -rf $(BUILDDIR)/*
{% endcodeblock %}

### MarkDown
{% codeblock sample.md https://github.com/kaedea GitHub %}
# hello world

you can write text [with links](http://example.com) inline or [link references][1].

* one _thing_ has *em*phasis
* two __things__ are **bold**

[1]: http://example.com

---

hello world
===========

<this_is inline="xml"></this_is>

> markdown is so cool

    so are code segments

1. one thing (yeah!)
2. two thing `i can write code`, and `more` wipee!
{% endcodeblock %}

### Nginx
{% codeblock sample..conf https://github.com/kaedea GitHub %}
user  www www;
worker_processes  2;
pid /var/run/nginx.pid;
error_log  /var/log/nginx.error_log  debug | info | notice | warn | error | crit;

events {
    connections   2000;
    use kqueue | rtsig | epoll | /dev/poll | select | poll;
}

http {
    log_format main      '$remote_addr - $remote_user [$time_local] '
                         '"$request" $status $bytes_sent '
                         '"$http_referer" "$http_user_agent" '
                         '"$gzip_ratio"';

    send_timeout 3m;
    client_header_buffer_size 1k;

    gzip on;
    gzip_min_length 1100;

    #lingering_time 30;

    server {
        server_name   one.example.com  www.one.example.com;
        access_log   /var/log/nginx.access_log  main;

        rewrite (.*) /index.php?page=$1 break;

        location / {
            proxy_pass         http://127.0.0.1/;
            proxy_redirect     off;
            proxy_set_header   Host             $host;
            proxy_set_header   X-Real-IP        $remote_addr;
            charset            koi8-r;
        }

        location /api/ {
            fastcgi_pass 127.0.0.1:9000;
        }

        location ~* \.(jpg|jpeg|gif)$ {
            root         /spool/www;
        }
    }
{% endcodeblock %}

### Object-C
{% codeblock sample.m https://github.com/kaedea GitHub %}
#import <UIKit/UIKit.h>
#import "Dependency.h"

@protocol WorldDataSource
@optional
- (NSString*)worldName;
@required
- (BOOL)allowsToLive;
@end

@interface Test : NSObject <HelloDelegate, WorldDataSource> {
  NSString *_greeting;
}

@property (nonatomic, readonly) NSString *greeting;
- (IBAction) show;
@end

@implementation Test

@synthesize test=_test;

+ (id) test {
  return [self testWithGreeting:@"Hello, world!\nFoo bar!"];
}

+ (id) testWithGreeting:(NSString*)greeting {
  return [[[self alloc] initWithGreeting:greeting] autorelease];
}

- (id) initWithGreeting:(NSString*)greeting {
  if ( (self = [super init]) ) {
    _greeting = [greeting retain];
  }
  return self;
}

- (void) dealloc {
  [_greeting release];
  [super dealloc];
}

@end
{% endcodeblock %}


### Perl
{% codeblock sample.perl https://github.com/kaedea GitHub %}
# loads object
sub load
{
  my $flds = $c->db_load($id,@_) || do {
    Carp::carp "Can`t load (class: $c, id: $id): '$!'"; return undef
  };
  my $o = $c->_perl_new();
  $id12 = $id / 24 / 3600;
  $o->{'ID'} = $id12 + 123;
  #$o->{'SHCUT'} = $flds->{'SHCUT'};
  my $p = $o->props;
  my $vt;
  $string =~ m/^sought_text$/;
  $items = split //, 'abc';
  $string //= "bar";
  for my $key (keys %$p)
  {
    if(${$vt.'::property'}) {
      $o->{$key . '_real'} = $flds->{$key};
      tie $o->{$key}, 'CMSBuilder::Property', $o, $key;
    }
  }
  $o->save if delete $o->{'_save_after_load'};

  # GH-117
  my $g = glob("/usr/bin/*");

  return $o;
}

=head1 NAME
POD till the end of file
{% endcodeblock %}



### PHP
{% codeblock sample.php https://github.com/kaedea GitHub %}
<?php
$heredoc = <<< HEREDOC_ID
some $contents
HEREDOC_ID;

function foo() {
   return SomeClass::$shared;
}

// Sample comment

class SomeClass extends One implements Another {
   private $my;
   public static $shared;
   const MAGIC = 0987654321;
   /**
    * Description by <a href="mailto:">user@host.dom</a>
    * @return SomeType
    */
   function doSmth($abc, $def) {
      foo();
      $def .=  self::MAGIC;
      $v = Helper::convert($abc . "\n {$def}" . $$def);
      $q = new Query( $this->invent(abs(0x80)) );
      return array($v => $q->result);
   }
}

interface Another {
}

include (dirname(__FILE__) . "inc.php");
`rm -r`;

goto Label;

Label:
<php_bad>№</php_bad>
{% endcodeblock %}



### Python
{% codeblock sample.py https://github.com/kaedea GitHub %}
@requires_authorization
def somefunc(param1='', param2=0):
    r'''A docstring'''
    if param1 > param2: # interesting
        print 'Gre\'ater'
    return (param2 - param1 + 1 + 0b10l) or None

class SomeClass:
    pass

>>> message = '''interpreter
... prompt'''
{% endcodeblock %}



### Ruby
{% codeblock sample.rb https://github.com/kaedea GitHub %}
class A < B; def self.create(object = User) object end end
class Zebra; def inspect; "X#{2 + self.object_id}" end end

module ABC::DEF
  include Comparable

  # @param test
  # @return [String] nothing
  def foo(test)
    Thread.new do |blockvar|
      ABC::DEF.reverse(:a_symbol, :'a symbol', :<=>, 'test' + ?\012)
      answer = valid?4 && valid?CONST && ?A && ?A.ord
    end.join
  end

  def [](index) self[index] end
  def ==(other) other == self end
end

class Car < ActiveRecord::Base
  has_many :wheels, class_name: 'Wheel', foreign_key: 'car_id'
  scope :available, -> { where(available: true) }
end

hash = {1 => 'one', 2 => 'two'}

2.0.0p0 :001 > ['some']
 => ["some"]
{% endcodeblock %}



### SQL
{% codeblock sample.sql https://github.com/kaedea GitHub %}
BEGIN;
CREATE TABLE "topic" (
    -- This is the greatest table of all time
    "id" serial NOT NULL PRIMARY KEY,
    "forum_id" integer NOT NULL,
    "subject" varchar(255) NOT NULL -- Because nobody likes an empty subject
);
ALTER TABLE "topic" ADD CONSTRAINT forum_id FOREIGN KEY ("forum_id") REFERENCES "forum" ("id");

-- Initials
insert into "topic" ("forum_id", "subject") values (2, 'D''artagnian');

select /* comment */ count(*) from cicero_forum;

-- this line lacks ; at the end to allow people to be sloppy and omit it in one-liners
/*
but who cares?
*/
COMMIT
{% endcodeblock %}



### HTML
{% codeblock sample.html https://github.com/kaedea GitHub %}
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2//EN">
<!--
*        Sample comment
-->
<HTML>
<head>
<title>WebStorm</title>
</head>
<body>
<h1>WebStorm</h1>
<p><br><b><IMG border=0 height=12 src="images/hg.gif" width=18 >
What is WebStorm? &#x00B7; &Alpha; </b><br><br>
</body>
</html>
{% endcodeblock %}



### Puppet
{% codeblock sample.pp https://github.com/kaedea GitHub %}
class hg_punch::library {

  firewall {'101 puppet library access':
    proto       => 'tcp',
    dport       => '80',
    action      => 'accept',
  }

  package { 'git':
    ensure => present,
  }

  vcsrepo { "puppet-library":
    path => '/var/www/puppet-library/',
    ensure => present,
    owner => 'root',
    group => 'root',
    provider => git,
    source => 'https://github.com/Moliholy/puppet-library.git',
    revision => 'master',
    require => Package['git'],
  }

  package { 'nfs-utils':
    ensure => present,
  }

  package { 'bundler':
    ensure => present,
    provider => gem,
  }

  package { [ "ruby", "ruby-devel", "gcc", "make" ]:
    ensure => present,
  }

  exec { 'bundler update':
    command => "bundler update && bundler",
    cwd => '/var/www/puppet-library',
    path => ["/usr/bin", "/bin", "/usr/sbin"],
    require => [ Package['ruby'], Package['ruby-devel'],
                Package['gcc'], Package['make'],
                Package['bundler'], Vcsrepo['puppet-library'] ]
  }

  package { 'mod_passenger':
    ensure => present,
  }

  file { "/etc/httpd/conf.d/puppetlibrary.conf":
    owner   => root,
    group   => root,
    mode    => 0644,
    content => template('hg_punch/puppetlibrary.conf.erb'),
    require => Package['mod_passenger'],
    selinux_ignore_defaults => true,
  }

  file { "/var/www/puppet-library/config.ru":
    owner   => root,
    group   => root,
    mode    => 0644,
    content => template('hg_punch/config.ru.erb'),
    require => Vcsrepo['puppet-library'],
  }

  file { [ '/var/www/puppet-library/public', '/var/www/puppet-library/tmp' ]:
    ensure => directory,
    owner   => root,
    group   => root,
    mode => 755,
    require => Vcsrepo['puppet-library'],
  }

  # Disable SELinux
  package { "augeas":
    ensure => present,
  }

  augeas {'disable_selinux':
    context => '/files/etc/sysconfig/selinux',
    changes => 'set SELINUX disabled',
    lens    => 'shellvars.lns',
    incl     => '/etc/sysconfig/selinux'
  } ~>
  exec {'sudo disable_selinux':
    command => '/bin/echo 0 > /selinux/enforce',
    refreshonly => true,
  }

  service { "httpd":
    enable => true,
    ensure => running,
    hasrestart => true,
    require => [ Exec['bundler update'],
                File['/etc/httpd/conf.d/puppetlibrary.conf'],
                File['/var/www/puppet-library/public'],
                File['/var/www/puppet-library/tmp'],
                Vcsrepo['puppet-library'],
                Package['mod_passenger'] ],
  }

}
{% endcodeblock %}



### LESS
{% codeblock sample.less https://github.com/kaedea GitHub %}
@import 'mixins'; // external mixins

@the-border: 1px;
@base-color: #111;

#header:after {
  color: @base-color * 3;
  border-right: @the-border * 2;
}

.colored(@c) when (iscolor(@c)) {
  color: (@base-color + #111) * 1.5;
}
@var: `"hello".toUpperCase() + '!'`;

@font-face {
  font-family: DroidSans;
  src: url(DroidSans.ttf);
  unicode-range: U+000-5FF, U+1e00-1fff, U+2000-2300;
}

div > p, p ~ ul, input[type="radio"] {
  color: green !important;
}
{% endcodeblock %}



### SCSS
{% codeblock sample.scss https://github.com/kaedea GitHub %}
.btn {
    font-size:      $font-size-base;
    background:     #fff;
    width:          auto;
    height:         auto;
    border-radius:  3px;
    letter-spacing: $letter-spacing-base;
    padding:        8px 15px;
    cursor:         pointer;
    margin:         0;

    &:hover,
    &:focus,
    &:active {
        text-decoration: none;
    }
}

// Colors variant
.btn--default {
    @include button-color-variant($font-color-light);
}
.btn--success {
    @include button-color-variant($color-success);
}
.btn--primary {
    @include button-color-variant($color-primary);
}
.btn--danger {
    @include button-color-variant($color-danger);
}

// Size variant
.btn--medium {
    @include button-size-variant($font-size-medium, 8px, 15px);
}
.btn--small {
    @include button-size-variant($font-size-small, 8px, 15px);
}

// States variant
.btn--disabled,
.btn--disabled:hover {
    color:           lighten($font-color-light, 10) !important;
    border:          1px solid lighten($font-color-light, 10);
    cursor:          not-allowed;
    text-decoration: none;
}
{% endcodeblock %}



### Stylus
{% codeblock sample.styl https://github.com/kaedea GitHub %}
@import "nib"

// variables
$green = #008000
$green_dark = darken($green, 10)

// mixin/function
container()
  max-width 980px

// mixin/function with parameters
buttonBG($color = green)
  if $color == green
    background-color #008000
  else if $color == red
    background-color #B22222

button
  buttonBG(red)

#content, .content
  font Tahoma, Chunkfive, sans-serif
  background url('hatch.png')
  color #F0F0F0 !important
  width 100%
{% endcodeblock %}



### Swift
{% codeblock sample.swift https://github.com/kaedea GitHub %}
extension MyClass : Interface {
    class func unarchiveFromFile<A>(file : A, (Int,Int) -> B) -> SKNode? {
        let path: String = bundle.pathForResource(file, ofType: "file\(name + 5).txt")
        let funnyNumber = 3 + 0xC2.15p2 * (1_000_000.000_000_1 - 000123.456) + 0o21
        var sceneData = NSData.dataWithContentsOfFile(path, options: .DataReadingMappedIfSafe, error: nil)
        /* a comment /* with a nested comment */ and the end */
    }
    @objc override func shouldAutorotate() {
        return true
    }
}
{% endcodeblock %}






