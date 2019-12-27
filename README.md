# log-go

应用开发中，日志使用者分为两类：

第一类是日志生产者，他们在开发过程中希望有简单明了的接口直接输出内容。
对他们来说全局接口往往是最好的体验，比如说Go标准库中提供的log库，
接口简单明了，撇一眼就知道如何使用而且不会犯错。

第二类是日志组织者，他们需要知道日志系统的实现，日志格式，日志输出地等具体细节。
他们要的往往是配置接口的灵活性。配置过程确实没那么直接，
但是往往一个工程中只要配置(设计)一次，后续开发就不需要再管了。

鉴于以上观点，日志设计应当被拆成两个不同的部分。一部分提供输出接口，另一部分
提供实现接口。

对比几个使用比较广泛的日志实现，都有或多或少的优缺点：

标准log库：接口足够明确但是过于简陋，无法做复杂的实现适配。

logrus：从接口角度，logrus满足所有需求，但是对比过zap的性能之后不免生出些嫌弃。

zap：性能无敌，但是不提供全局接口。

即想要logrus的接口又想要zap的性能，就只能自己拼了。

log-go提供一个极简但基本覆盖大部分日志生产者需求的接口，并提供标准的适配方式，
可以将现成的日志库适配到系统中。配置者直接选择他们想要的日志系统实现，
在所选择的实现系统中做配置，之后再做一次简单适配即可集成进来。

log-go只需要关注自身代理实现的性能，不要对实现系统产生过多的性能损耗即可。

