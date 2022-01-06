### 什么是性能测试
* 性能测试
** 性能测试是指在给定条件基准的前提下能达到的运行程度，测试软件在系统中的运行性能，度量系统与预定义目标的差距。
** 负载测试、容量测试、压力测试、强度测试都属于性能测试，
* 性能测试-负载测试
** 负载测试是模拟在超负荷环境中运行，通过不断加载（如逐渐增加模拟用户的数量）或其它加载方式来观察不同负载下系统的响应时间和数据吞吐量、系统占用的资源（如CPU、内存）等，以检验系统的行为和特性，以发现系统可能存在的性能瓶颈、内存泄漏、不能实时同步等问题。负载测试更多地体现了一种方法或一种技术。
* 性能测试-压力测试（强度测试）
** 压力测试是在强负载（大数据量、大量并发用户等）下的测试，查看应用系统在峰值使用情况下操作行为，从而有效地发现系统的某项功能隐患、系统是否具有良好的容错能力和可恢复能力。压力测试分为高负载下的长时间（如24小时以上）的稳定性压力测试和极限负载情况下导致系统崩溃的破坏性压力测试。
* 性能测试-容量测试
** 通过测试预先分析出反映软件系统应用特征的某项指标的极限值（如大并发用户数、数据库记录数等），系统在其极限值状态下没有出现任何软件故障或还能保持主要功能正常运行。容量测试是面向数据的，并且它的目的是显示系统可以处理目标内确定的数据容量。
* 例：一个人背X斤
** 负载测试：200斤情况下，是否能坚持5分钟。
** 压力测试：200，300，400... 斤情况下，他的表现，什么时候失败，失败之后什么表现，重新扛200是否正常。
** 容量测试：在坚持5分钟的情况下，他一次多能扛多少斤。

== 目的 ==
* 验证系统是否满足预期需求(验证系统的性能指标是否满足既定值);
* 验证系统在高压下的表现;
* 验证系统是否能持续稳定的运行;
* 探测系统的瓶颈和产生瓶颈的原因，探测系统设计与资源之间的最佳平衡，改善并优化系统的性能。
* 使性能工程成为一个迭代的过程，客观地说，压力测试和性能工程是“永无止境”的。由于从应用程序的工作负载、到功能服务、再到体系架构中的几乎每个组件，我们都需要对它们进行持续的开发与部署，因此就算是某个新增的简单变更，也可能会对前期的性能测试结果带来干扰。所以说，性能测试应当随着应用程序的迭代而继续。

== 压力测试常用考核指标 ==
* 资源利用率：主要是针对web服务器、操作系统等系统资源的使用程度，这也是为了改善系统性能的重要依据。
* 系统性能指标
**响应时间（RT，单位毫秒）：指该系统所有功能的平均响应时间或者所有功能的最大响应时间，互联网行业标准为500毫秒以下，但软件性能的高低实际上取决于用户对该响应时间的接受程度。
**系统处理能力：指系统在利用系统硬件平台和软件平台进行信息处理的能力。
***TPS（Transaction per second）：系统每秒处理交易数（事务数）（笔/秒）。
***QPS（Query per second）：系统每秒处理查询次数（次/秒）。
***HPS（Hits Per Second）：每秒点击次数（次/秒）。
***RPS（每秒请求数）、EPS。
****对于互联网业务中，如果某些业务有且仅有一个请求连接，那么TPS=QPS=HPS。
****一般情况下用TPS来衡量整个业务流程，用QPS来衡量接口查询次数，用HPS来表示对服务器点击请求(数值越大越好)。
****QPS = 1000*线程数量/RT。QPS 单位是秒，RT单位是毫秒，单位换算分子需要乘1000。QPS 和 RT 成反比，当超过最佳线程数，会导致资源竞争加剧，同时响应时间也会增加，QPS 下降。
****TPS互联网行业标准：小型网站: 500TPS~10000TPS；中型网站：1000TPS~50000TPS；电子商务：10000TPS~1000000TPS。
**并发用户数：指在同一时刻内，登录系统并进行业务操作的用户数量。并发用户数对于长连接系统来说最大并发用户数即是系统的并发接入能力
**错误率：指系统在负载情况下，失败交易的概率。
***错误率＝(失败交易数/交易总数)*100%。稳定性较好的系统，其错误率应该由超时引起，即为超时率。
***不同系统对错误率的要求不同，但一般不超出千分之六，即成功率不低于99.4%
**吞吐量：指在无网络故障的情况下单位时间内通过的网络的数据数量，单位为Byte/s。
***吞吐量指标用于衡量系统对于网络设备或链路传输能力的需求。当网络吞吐量指标接近网络设备或链路最大传输能力时，则需要考虑升级网络设备。
*资源性能指标
**CPU使用率、内存利用率、JVM堆栈使用情况、GC/FGC次数、Load指标（CPU负载，CPU使用队列的长度的统计信息）、网络吞吐量、网络延时（常用应用服务器ping数据库，观察数据库延时是多少）
*数据库指标
**常用的数据库例如MySQL指标，主要包括缓存命中率、连接数、数据库的操作监控等。
* 其他：压测请求成功率、比如在试压情况下系统的响应时间（web请求处理完毕的时间）等。
** th99、th95、avg

== 注意事项 ==
* 禁止压测的接口
** <font color=#f5222d>涉及短信发送</font>
** <font color=#f5222d>涉及推送</font>
** <font color=#f5222d>涉及第三方支付</font>
* 测试环境的搭建
** 如果计算机软硬件平台的配置跟不上，那对测试结果也会有很大的影响。
* 性能测试使用的测试数据需要尽可能接近真实数据。
* 测试顺序先使用单线程进行性能基准测试，再进行压测，每项压测后使用基准测试与压测测试数据进行对比。
* 单线程与多线程做数据对比时，务必保证每线程内的数据量时相等，保证可比性。
* 网络带宽测试，能否满足网络流量需求。
* 其他 
** 性能测试所需文档至少有《接口文档》、《性能指标文档》、《测试大纲》。
* 性能测试报告
** 务必说明测试环境及测试数据。
** 报告中每张图都要有响应解读分析，明确说明图的用意及参数说明情况。
** 测试完成后要给出测试情况分析，尤其要指出本次测试中不符合性能指标的部分并要告知是否提交bug，bug描述清楚。
** 最后要给出测试结论，测试是否通过。
* 测试原则
** <font color=#f5222d>第一个原则</font>，就是性能测试只有在实际项目中实施才是有意义的，这样才使得测试工作具有针对性，而且目标会更加明确。
*** 微观基准，可以理解为在某一个方法或某一个组件中进行的单元性能测试。
**** 检测一个线程同步和一个非线程同步的方法运行时所需要的时间。
**** 对比创建一个单独线程和使用一个线程池的性能开销。
**** 对比执行一个算法中的某一个迭代过程所需要的时间
*** 宏观基准，当我们测量应用程序性能时，应当纵览整个系统，影响应用程序性能的原因可能是多方面的，不能片面的认为性能瓶颈只会在程序本身上。
*** 折衷基准，相比微观基准和宏观基准，一个单独功能模块的性能测试，或者一系列特定操作的性能测试被称为折衷基准。它是介于微观基准和宏观基准之间的折衷方案。基于微观基准测试的正确性是较难把握的，性能瓶颈的判断绝不能仅仅依赖于此。如果我们要使用微观基准作为性能的测量方法，那么不妨在此之前先尝试基于宏观基准的测试。它可以帮助我们了解系统以及代码是如何工作的，从而形成一个系统整体逻辑结构图。接下来可以考虑基于折衷基准的测试，来真正发现潜在的性能瓶颈。需要明确的是折衷基准的测试方法并不是完整应用程序测试的替代方法，更多情况下我们认为它更适用于一个功能模块的自动测试。
** <font color=#f5222d>第二个原则</font>，引入多样的测量方法来分析程序的性能。
*** 批量执行所用时间的测量方法（耗时法），这是种简单而快速有效的方法，通过测量完成特定任务所消耗的时间来测量整体性能。但是需要特别注意，假如所测试的应用程序中使用缓存数据技术来为了获得更好的性能表现时，多次循环使用该方法可能无法完全反应性能问题。那么可以尝试在初始状态开始时应用耗时法做一次性能的评估，然后当缓存建立后，再次尝试此方法。
*** 吞吐量的测量方法，在一段时间内考察完成任务的数量的能力，被称为吞吐量测量方法。在测试客户服务器的应用程序时，吞吐量的测量意味着客户端发送请求到服务器是没有任何延迟的，当客户端接收到响应后，应当立即发出新的请求，直到最终结束，统计客户端完成任务的总数。这种相对理想的测试方法通常称之为“Zero-think-time”。
*** 响应时间的测量方法，响应时间的测量方法是指客户端发出一个请求后直到接收到服务器的响应返回后的时间消耗。响应时间测量方法不同于吞吐量测量方法，在响应时间测试过程中，客户端线程可能会在操作的过程中某一时刻休眠，这就引出“think- time”这个关键词，当“think- time”被引入到测试过程中，也就是意味着待处理任务量是固定的，测量的是服务器响应请求的速率是怎样的。大多数情况下，响应时间的测量方法用来模拟用户真实操作，从而测量应用程序的性能。
** <font color=#f5222d>第三个原则</font>，理解测试结果如何随时间改变，即使每一次测试使用同样的数据，可能获得的结果也是不同的。一些客观因素，比如后台运行的进程，网络的负载情况，这些都可能带来测试结果的不同，所以在测试过程中存在着一些随机性的因素。

== 测试的一般流程 == 
* 准备工作  先要确定在什么阶段开展性能测试工作，该使用哪些工具，具体的分工是怎样的。
* 性能测试计划 要分析性能测试背景，用户场景，性能目标，以及制定性能测试实施计划。
* 性能测试设计 具体包括了测试环境设计，测试场景设计，测试用例设计 ，编写测试脚本 
* 性能测试执行 先部署好测试环境 一般由运维或开发人员进行环境的部署，并进行资源协调。然后执行测试脚本按照业务场景和测试用例，按顺序执行我们已经设计好的测试脚本。 接着进行性能监控和记录。
* 性能测试分析 分析不同的测试环境下，硬件设备的性能指标与预期的性能指标进行对比，确定是否达到了我们需要的结果。
* 性能测试调优 确定问题：根据性能分析结果确定存在的性能问题。 然后分析问题根据确定的问题进行具体详细的分析出现问题的原因进行调整，使分析调优结果达到预期目标。
* 性能汇总与报告 对性能测试的过程和结果进行汇总 编写性能测试报告。

== 如何使用APM开展有序的压力测试，并进行规范性的根本原因分析 ==
* 第1部分：设置基线并确定当前容量?
** 我们的首要任务就是先构造压力测试，然后缓慢增加负载，直至应用程序出现瓶颈。
** 1，我们从最小用户数的负载开始(例如：5个用户的并发量)，执行至少持续一小时的压力测试。我们将这种低负载测试的结果作为一个基线。如果针对基线压力测试的结果，已经能够出现并发的事务超出了服务级别协议(SLA)，那么我们就没有理由再进行下一步的可伸缩性测试了。而如果一切正常，我们则继续下一步。
** 2，通过基线压力测试的结果，您可以为应用设置可接受的Apdex分数（该Apdex是目标应用程序平均响应时间的标准）。
** 3，设计并执行压力测试，然后有条不紊地增加用户数量。请为每一个应用程序设计不同的吞吐量和用户负载目标。例如，您可以使用5个并发用户数来触发压力测试，接着每隔15秒钟再添加5个用户。随着用户数量的增加，压力测试将慢慢接近性能的临界点，这将使您能够了解到目标应用程序所能够处理负载的极限。（记住：压力测试应当被设计为有序进行，而不要一股脑地将目标工作负载抛给应用程序，否则得到的结果不但混乱、且难以解释。例如：如果您的目标是达到5,000个并发用户，那么您设计的压力测试应当先锚定该目标的一半。如果此应用能够成功地扩展到目标负载的一半，那么您才可以继续设计下一轮测试，以使负载加倍。同样，如果您测试的是负载吞吐量，而不是用户数与活动会话，那么您仍然可以使用相同的方法稳健地达到目标所设定的每秒事务数。例如，如果您的API吞吐量目标为每秒200个事务的话，那么您可以逐步将测试的压力扩展到每秒100个事务）。
** 4，在应用程序的APM概览页面中来查看“事务分位数(transactions percentiles)”。由于其中95%的记录都会比中位或平均值更加敏锐与精细，因此您可以将主要精力集中在这95%的记录行上。通过观察，您可以找到目标应用在压力测试下开始出现服务质量下降的时间点，然后突出显示并放大该时间范围与跨度，以便您能够执行更为深入的分析。例如，您可以深入挖掘各种事务性、分布式的轨迹、以及相关的错误(记住：该测试部分的主要目标是首次识别瓶颈，因此您不需担心在首次拐点之后的图表走势。任何跨过该点的状态，都只是某个根本原因的后续症状而已)。
* 第2部分：隔离首个瓶颈
** 针对上述发现的性能下降情况，您可以根据应用的实际情况，执行如下步骤5到9(可以不一定按照该顺序)以进行问题排查。例如，您可以从分析响应的时间开始，顺藤摸瓜，直到发现APM中的代码缺陷(也就是所谓的自上而下的方法)。
** 5，利用在步骤4中所收集的信息，采用“全链路追踪（宏观），亦或是微服务网络拓扑图”来识别到底是哪个应用事务的哪些内、外部服务水平出现了下降，并导致了总体响应时间的增加（如果您发现有多个事务存在着服务水平的下降趋势，那么这通常表明有某些资源已经接近到了它们的饱和点）。
** 6，使用APM来逐步隔离各种代码的缺陷、或是错误的条件。使用“全链路追踪（微观）”方法，来隔离服务降级、或是抛出错误的确切代码。
** 7，识别基础架构中诸如Web服务器、JVM或数据库等方面的限制。
** 8，检查应用部署所涉及到的每一台主机和服务器，以查看是否有硬件资源(CPU、内存、以及网络等)被滥用的情况（硬件资源不一定是在完全饱和时，才能导致响应时间的延长。有时候，达到70%的饱和度时，其性能就会受到影响。如果您在压力测试中发现瓶颈并非源自硬件资源，那么就请检查服务器的软件资源，其中包括：连接池、数据源连接数、及其TCP堆栈等方面。因为当软件资源饱和时，它们同样会在基础架构中出现“排队”的状况）。
** 9，确定响应时间的增加是否来自应用的前端。例如，当您的站点需要呈现某些HTML类资产时，那些向第三方远程服务器发送的Ajax请求数，就有可能会导致整体速度的下降。
* 第3部分：优化以缓解瓶颈问题
** 在确定了瓶颈的原因之后，您需要通过实施变更，来应对新的压力测试。
** 10，对于应用程序的任何变更，您都需要予以记录。您可以使用诸如：“向VM增加了2颗CPU”之类详细信息，来标记针对某次变更的部署（记住：一次仅修改一个变量。如果您一次性地修改了两个、或更多的内容(例如，增加了多个硬件资源、并让JVM堆栈的大小翻倍了)，那么您将无从知晓到底是哪个变量，如何影响了应用程序的总体负载性能）。
** 11.重新运行压力测试并分析新的结果，以判断性能是否有所改观。如果没有任何差异的话，那就意味着您并未找到真正的瓶颈。请保留或还原先前的变更，并按需重复前面的测试步骤。
** 12.持续进行压力测试，直至真正消除了瓶颈，并满足了既定的各项负载需求。
