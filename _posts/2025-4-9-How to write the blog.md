# About the details of writing blog
As a newcomer who has never blogged before, even after generating my first blog, there are still a lot of details that I can't quite understand, so I'm writing this blog to document how to use this platform.

First is the meaning of folder:  
- _config.yml: Global Configuration File  
- _posts Folders: for blog posts  
- img: The folder where the pictures are stored  

The blog post format is MarkDown + YAML, so let's find out how these two formats should be written!  

## YAML
### mapping
A set of key-value pairs for an object, using a colon structure animal: pets   
Yaml also allows another way to write all key-value pairs as a single in-line object. hash: { name: Steve, foo: bar } 

### arrays
A set of lines beginning with a hyphenated line forms an array.
- Cat
- Dog
- Goldfish
Arrays can also be represented in-line.  
animal: [Cat, Dog]

### scalars
String: strings are not quoted by default, if the string contains spaces or special characters, they need to be put in quotes.  
Boolean: true and false.   
Integer/Float: values are expressed directly as literals.  
Null: indicated by ~.   
Time: use ISO8601 format   
Date: date is expressed as year, month and day in composite iso8601 format.   

### References
Anchors & and aliases *, can be used for references.

The tutorial can be found at  https://www.runoob.com/w3cnote/yaml-intro.html

## MarkDown
https://markdown.com.cn/basic-syntax/
