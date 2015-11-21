[1、riak_sysmon](https://github.com/basho/riak_sysmon)

对erlang:system_monitor/0,1,2的封装，尽快的发现系统中存在的long_gc，large_heap等性能隐患。针对上述痛点中的“refc binary”和“OOM”。

[2、recon](https://github.com/ferd/recon)

封装了erlang:process_info/1,2函数，并提供了TOPN的feature，recon_alloc封装了度量虚拟机内部内存的使用量的查询。
不仅如此，recon提供了一种近似度量Erlang进程CPU消耗的方案，Erlang tool --recon，memoryleak的检查。针对上述痛点中的“Erlang进程CPU消耗度量”、“refc binary”，并且提供了种种便利。好用到爆的感觉。

[3、eper/redbug](https://github.com/massemanet/eper)

刚开始接触Erlang时，社区提供的一种代码调试方案是日志。然，这种方式太不优雅，使用起来非常麻烦。
redbug是对Erlang系统中dbg模块的封装，提供了非常安全有效的代码调试方式。“安全”对生产环境来说，确实太过重要了。

[4、pooler/poolboy](https://github.com/seth/pooler)

github : [seth/pooler · GitHub](https://github.com/seth/pooler)

github :[ devinus/poolboy · GitHub](https://github.com/devinus/poolboy)

池。Erlang单进程效率的问题，非常常见的三种方式，第一种是池，第二种是noblock call，第三种是修改某个进程的资源配置。
在社区中，常见的是第一种方案，而第二种和第三种方案常见于Erlang编程语言编源码中（rpc模块，net_kernel模块）。针对上述痛点中的“单进程问题”。

[5、jiffy](https://github.com/davisp/jiffy)

github : davisp/jiffy · GitHub
json处理库，而且是nif的，能够尽可能保证效果，并且可以支持return_maps已经encode force_utf8，decode 的return_maps能直接返回map 数据类型，非常之方便。（虽然17的map效率不怎么样，但是18版本做了很大的优化）

[6、entop](https://github.com/mazenharake/entop)

github : mazenharake/entop · GitHub
有没有觉得Erlang自带的etop有些难用？entop提供了非常不错的可替代方案。

[7、erlang-lz4](https://github.com/szktty/erlang-lz4)

github : szktty/erlang-lz4 · GitHub
不管是Erlang系统，还是其他系统，所倡导的都是“小消息，大计算”，加之Erlang消息传递是值传递的方式，对于大的message，稍微做一下压缩，获取能取得意想不到的效果。不放试一试，lz4 的算法，请Google 之。

[8、sync](https://github.com/rustyio/sync)

github : rustyio/sync · GitHub
on-the-fly recompiling and reloading in Erlang. 大幅度提高工作效率，避免接二连三的重新compile、generate。不过，要注意的是，最好只用在开发环境下。
关于热更，多叨叨两句：
> 1，在supervisor下增删 gen_server child 热更会失败，目前无解，除非修改supervisor源代码
> 2，gen_server record 增删字段，这个可用 “使用proplists字段值”或者是“map字段值”
> 3，gen_server init 函数逻辑无法热更，解决办法，重写code_change 代码
> 至于常规的逻辑代码，热更基本上没什么问题

[9、erlang_term](https://github.com/okeuday/erlang_term)

github : okeuday/erlang_term · GitHub
存了一个Term到ETS表中，难道不应该知道这个Term到底占用了多大的内存空间吗？要send一个大的message给另一个进程，不度量一点内存占用大小就随心所欲？恐怕不太好。erlang_term可以作为贴心小工具。[Erlang ets -- something about cache continue](http://www.cnblogs.com/--00/p/erlang_ets_something_about_cache_continue.html)

[10、folsom](https://github.com/boundary/folsom)

github : boundary/folsom · GitHub
提供了多种Metrics 模型，根据自己的应用场景，选择不同的模型就行。内部主要使用ets:update_counter/3,4，性能效果很有保证。

[11、ej](https://github.com/seth/ej)

github : seth/ej · GitHub
Helper module for working with Erlang terms representing JSON
试试就知道有没有意思，好不好玩了。

[12、task](https://github.com/redink-toys/task)

github : redink-toys/task · GitHub
遇到过这样一个有意思的场景：主进程是一个普通进程，有10W量级的列表，我想将其过滤之后，将1/2或者是1/4的列表写入到ETS表中，然后进行后续的操作。如果我在主进程中做这一些列操作，这个主进程就会被挂住，因为GC（Erlang的GC不会STW，但很有可能会STP）。考虑到ETS表可以在不同的进程之间共享数据，我就可以在主进程中spawn一个进程，这个这个进程去执行过滤、写入操作，然后这个进程生命周期结束之后，GC是很简单快速的。
task就是一个spawn、receive的简单封装。

[13、xref_runner](https://github.com/inaka/xref_runner)

github : inaka/xref_runner · GitHub
[做xref检查：善待Erlang 代码 -- Xref 实践](http://www.cnblogs.com/--00/p/code_erlang_xref.html)

[14. inaka/elvis](https://github.com/inaka/elvis)

Erlang代码style检查，支持github webhook，支持Erlang shell内运行检查。另外inaka/erlang_guidelines提供了对初学者很友好的style guide，对一开始养成良好的代码格式用处很大。

[15. inaka/xref_runner](https://github.com/inaka/xref_runner)

跑xref的， @redink 已经安利过了

[16. inaka/apns4erl](https://github.com/inaka/apns4erl)

久经考验的iOS APNS推送服务

[17. inaka/shotgun](https://github.com/inaka/shotgun)

对ninenines/gun的封装，支持SSE (Server-sent Events) handling

[18. inaka/worker_pool](https://github.com/inaka/worker_pool)

提供比poolboy更轻量的worker pool实现，支持多种worker轮转策略

其中whisper1, tigertext, inaka是我司和友司的Github，欢迎围观，其中inaka是最有料的repo。

再安利一个[Erlang Makefile](https://github.com/ninenines/erlang.mk) ，虽然现在和一些项目不兼容而且功能还不完善，但和rebar相比，erlang.mk极大的提高了并发编译的速度。换了Erlang.mk之后感觉编译速度快了几倍。


说个坑。
[benoitc/hackney](https://github.com/benoitc/hackney) 是个坑。Hackney是个坑。Hackney是个坑。虽然拼multi-part很好用，但是建议只使用hackney_lib里提供的函数封装，再使用别的http库发。Hackney pool有很多不可复现的未知问题。
