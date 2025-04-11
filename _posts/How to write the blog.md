# About the details of writing blog
作为一个从未写过博客的新人，哪怕生成了第一篇博客，还是有很多细节上不太能理解，因此写此篇博客来记录如何使用这个平台。
首先是文件夹的含义
_config.yml 全局配置文件
_posts 放置博客文章的文件夹
img 存放图片的文件夹
博客文章格式采用是 MarkDown+ YAML 的方式，所以我们接下来了解这两个的格式应该怎么写

## YAML
### mapping
对象的一组键值对，使用冒号结构表示 animal: pets
Yaml 也允许另一种写法，将所有键值对写成一个行内对象。hash: { name: Steve, foo: bar } 
### 数组
一组连词线开头的行，构成一个数组。
- Cat
- Dog
- Goldfish
数组也可以采用行内表示法。
animal: [Cat, Dog]
### scalars
字符串：字符串默认不使用引号表示，如果字符串之中包含空格或特殊字符，需要放在引号之中。
布尔值：用true和false表示。
整数/浮点数：数值直接以字面量的形式表示。
Null：用~表示。
时间：采用 ISO8601 格式
日期：日期采用复合 iso8601 格式的年、月、日表示。
### 引用
锚点&和别名*，可以用来引用。如
defaults: &defaults
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  <<: *defaults

test:
  database: myapp_test
  <<: *defaults
  等同于
defaults:
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  adapter:  postgres
  host:     localhost

test:
  database: myapp_test
  adapter:  postgres
  host:     localhost
