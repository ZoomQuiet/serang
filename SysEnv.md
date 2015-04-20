SeRang
# 系统环境 #
主要是MachineNode上的环境

# 用户开发平台 #
运行在AE上的应用要符合AE的要求，这跟AE中每台提供服务的机器上运行的环境有密切关系。这里主要是贴近已有的成功方案，跟风。
开发语言
AE中提供服务的机器，要连续不断的提供服务，不会因为应用的发布而重启。基于一种解释性的语言，会比需要编译的语言更适合。比如python，python相关的框架很多，适合作web开发，当然php也不错
初步

  1. python

开发框架
根据选择的语言决定。AE的重点在于如何能维持住各种不同的应用（当然，这些应用一定在AE的约定范围内开发的），而不是开发框架。选择现有的比较成熟的框架作为AE程序的基础，在此之上要做的事情是，提供对AE基础资源的访问入口。GAE使用django和webob作为基础的框架，同时说能够支持所有的主流python开发框架(和python的性质有关)
初步

  1. django
  1. webob
  1. sqlalchemy,相对sqlobject，sa更活跃，TG也从so转到了sa。dataStore可用之前，使用mysql测试，之后需要对dataStore封装python接口