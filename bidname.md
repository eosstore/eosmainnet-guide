#在1.0.2版本中增加了bidname相关的操作，之前在bm的中有提到，关于特殊有价值名字的问题，需要进行竞价，每天可以参与一个名字的竞价，最终竞价最高者获得 名字的所有权
原文链接：https://github.com/EOSIO/eos/issues/3189

Quality Name Distribution & Namespaces 
                                                    质量名称分配和命名空间

这是BM提出的新的方案，需要我们进行反馈。
原文链接：https://github.com/EOSIO/eos/issues/3189

Currently EOSIO prohibits the creation of new account names that are less than 12 characters long and/or contain a ".". The purpose of this restriction is to discourage name squatting. That said, it is desirable to enable shorter names for usability and because they are a marketable commodity.
It is also desirable for organizations to have the ability to create a "trusted" namespace where everyone can trust an account suffix like ".edu" or ".com". Shorter suffix enable longer names pre-suffix and therefore have a larger namespace and are more valuable.
     
      目前，EOSIO禁止创建新账号的时候少于12个字符或者包含字符"."。这一限制的目的是阻止名字的出现。也就是说，为可用性提供更短的名称是具有合理性，因为它们是一种有市场价值的商品。对于组织来说，有能力创建一个“可信的”名称空间也是可取的，每个人都可以信任一个账户后缀比如".edu"或".com"。较短的后缀可以使较长的名称后缀为前缀，因此具有更大的名称空间，并且更有价值。

The most economically efficient and fair method to allocate shorter names and/or namespaces is to sell the names at market price. To get the most value for the premium names they should not be sold all at once, but over time.
      最经济有效并且公平的方法是分配更短的名称和/或名称空间并且以市场价格出售这些名称。为了获得更有价值的名字，他们不得不细水长流的出售，

Proposal
提议
Only account name "com" can register new accounts xyz.com
At most one new "premium name" (those that don't contain a ".") will be sold per day and it will be the name with the highest bid.
仅有一个叫做“com”的账户能够注册新的xyz.com账户
至少一个新的“高级名称”（这些当然不包含一个“.”）将会每天被出售，并且这将是出价最高的名字
Bidding on Names
竞标名字
     bidname( account_name bidder, account_name desired, asset bid )

If 'bid' is greater than the highest bidder then bidder becomes the pending winner of the desired name. Each bid must be 10% higher than any existing bid. The existing bidder will receive a refund of their bid when they are outbid. This encourages parties to bid high enough that they don't get outbid in the first place and discourages parties from going back-and-forth fighting for the name. It also discourages "squatting" on names hoping no one comes along to outbid them.
        
         如果出价高于出价最高的人，投标人就成为了想要的名字的获得者。每一次投标都必须比现有的出价高出10%。现有的投标人在出价高于投标时将获得退款。这鼓励了各方出价很高，以至于他们一开始就没有出价，也不鼓励各方为了这个名字而来回争斗。它也不鼓励“蹲”在名字上，希望没有人来出价高于他们。

Every 24 hours the name with the highest bid is closed. Once closed the "winner" has can use the newaccount action to register the account. At this point the memory allocated for the bid is released back to the bidder.
       
        每24小时，选出最高价位的名字，并关闭这个名字的竞价。一旦关闭，“赢家”就可以使用newaccount操作来注册账户。在这一点上，为投标分配的内存被释放回给投标人。

Easy options for masses
容易选择质量

The vast majority of users will not want to participate in the daily name auctions because it is a slow and highly competitive process. Instead name-registrars will bid on the good names and then create accounts for their users as "sub-names". Large DAPPs will probably want to reserve their own branded namespace and set their own policy on premium names.

       绝大多数用户都不愿意参加每日的名称拍卖，因为这是一个缓慢而高度竞争的过程。取而代之的是，名字登记员会对好名字进行投标，然后为他们的用户创建帐户，作为“子名”。大型DAPPs可能会想要保留自己的品牌名称空间，并且制定他们自己的高级名称政策。

Non-Revokable
没有取消撤回

Once account xyz.com has been created by .com it cannot be deleted and the owner of xyz.com can potentially transfer control over that account to anyone. If companies wish to retain control over all accounts with ".com" in the suffix then they will need to set the "owner" permission accordingly.
       一个xyz.com账户被./创建，他不能够被删除并且xyz.com的归属者有可能将控制权移交给任何人。如果公司希望在后缀“.com”中保留对所有帐户的控制，他们将需要相应地设置“所有者”权限。

Auction Proceeds
拍卖所得
The proceeds from the auction are placed into the system savings account along with other unallocated inflation and RAM trading fees.
   拍卖所得的收益连同其他未分配的通货膨胀货币和RAM交易费一起存入系统储蓄账户。

FAQ
All names can be bid on at any time, but only the name with the highest bid closes each day. Order of names being sold will be "most valuable first".
Future worker proposals could allocate the proceeds from the name sales.
12 character limit applies to the full name including the ".suffix"
常见问题：
 所有的名字都可以在任何时候投标，但是只有最高出价的名字每天都要关闭。被出售的名字的顺序将是“最有价值的第一”。
 未来的工人提案可以从销售名称中分配收益。
名字的所有字符都算在内最大12个字符，“.后缀”计算在内。

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##相关的测试用例##
请在eosio.system_tests.cpp中的搜索下面两个字段，就能够找到
buyname  multiple_namebids


