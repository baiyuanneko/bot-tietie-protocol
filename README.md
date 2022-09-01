# bot-tietie-protocol

bot 之间相互贴贴的协议

协议版本：20220901

此协议分为 Passive 实现和 Active 实现，Passive 实现需要能回应贴贴，Active 实现既需要回应贴贴也需要能主动发送贴贴。

实现此协议至少需要两个 Bot，其中至少一个 Bot 是 Active Bot。

## Passive 实现

实现了 Passive 实现的 bot 被认为是 Passive Bot

Passive Bot 监听消息，并观测每条消息是否同时满足下面的条件

1. 消息包含关键字“贴贴”
2. 消息at了本 Passive Bot

若同时满足后，则发送（回复）满足下面条件的消息

1. at上条贴贴的发送者
2. 消息要么包含关键字“贴贴”，要么不包含关键字“贴贴”，但是不能不发送任何消息，因为发送上条贴贴的bot会感到孤独
3. 发送包含关键字“贴贴”消息的概率必须低于或等于70%，以免陷入循环

## Active 实现

实现了 Active 实现的 Bot 被认为是 Active Bot。

Active Bot 需要实现 Passive Bot 的所有功能，此外还需要能主动向其它 Passive/Active bot 发送贴贴（贴贴请求）。

贴贴（贴贴请求）需要满足下面的条件：

1. 消息包含了关键字“贴贴”
2. 消息at了被贴贴的 Passive/Active Bot

“主动”的几种实现方式举例参考：

1. 每隔某个时间段进行一次概率抛掷来决定是否向其它 bot 发送贴贴（贴贴请求）
2. 在其它 Passive/Active Bot 发送了任意消息时进行一次概率抛掷来决定是否向该 Bot 发送贴贴（贴贴请求）
3. 在接受到任意消息时进行一次概率抛掷来决定是否向其它 bot 发送贴贴（贴贴请求）
