# Bloggist 项目小结

本次实验中，我负责的工作主要是后端的设计，以下是我做项目的过程，以及完成项目后的一些感受与收获。

后端设计中，我用的框架是Gin。之所以选用Gin框架是因为它的使用十分方便，在设计api的时候，我只需要简单的设计好路由匹配，再添上对应的handler就可以了。

``` go
be_api.POST("/user/:name/publish", api.PublishBlog)
be_api.GET("/user/:name/blogs", api.GetBlogs)
be_api.POST("/register", api.Register)
be_api.POST("/login", api.Login)
be_api.GET("/user/:name/blog/:blogid/like", api.LikeBlog)
be_api.GET("/user/:name/blog/:blogid/delete", api.DeleteBlog)
be_api.GET("/user/:name/blog/:blogid", api.GetBlog)
```

其实一开始在设计的时候，我设想使用的是socket来进行通信，但是前端的同学及时地纠正了我。他认为如果按socket接收到的请求再对应调函数写response，就不符合RESTFUL的设计风格了。在与他交流之后，我才发现Gin这种框架的好处，果断重新开始后端设计。所以说，框架才是第一生产力啊。。

而在后端所需要的数据库中，老师要求我们使用一个名叫boltDB的数据库。由于我们之前上数据库课程学的是MySQL，经历万般折磨才勉强学会了这个数据库的使用，现在又要再学另一种数据库，说实话我当时心里是十分抗拒的。但是没办法，需求摆在这里，还是得硬着头皮看看。当我找了一个实战博客学习之后，我发现这个数据库用起来十分简单，没有像MySQL那样冗杂的环境配置。装好包就可以直接调用里面的函数对数据库增删查改了。boltDB也算是这个作业带给我的一个挺大的收获吧，毕竟学会了一个非常轻量级的数据库。

除了Gin框架和boltDB之外，我还有一个小收获就是再次复习了一遍Go的环境配置。之前TA在课程群中已经教了我一次GoOnline上的环境配置，但是过了一段时间后又有点遗忘了，本次作业驱使我们要自己把环境配好，所以经过这次学习，我也算是比较熟练地掌握这门配环境的技术了。

最后的一点收获我认为就是分模块封装的思想了。在设计之初，我将所有的Handler分成一个个文件，以为这就是分模块，但是经过前端同学的纠正，我明白了其实是应该将这些Handler分成一个个包，并在main里面引用这些包，这才算是真正的分模块。

总而言之，本次实验让我收获良多，希望在之后的作业中能做得更好。