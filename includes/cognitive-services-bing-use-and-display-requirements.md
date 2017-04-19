以下使用和显示要求适用于特定内容和关联信息（例如关系、元数据和其他信号）的实现，这些内容和信息是通过调用必应 Web 搜索、图片搜索、视频搜索和新闻搜索 API 以及必应拼写检查 API 和必应自动推荐 API 获取的。 与这些要求相关的实现细节可在特定功能和结果的文档中找到。

## <a name="1--bing-spell-check-api-and-bing-autosuggest-api--you-must-not"></a>1.必应拼写检查 API 和必应自动推荐 API。  你不得：

- 复制、存储或缓存从必应拼写检查或必应自动推荐 API 接收的任何数据；或者为了训练、评估或改进你或者第三方可能会提供的新服务或现有服务，而在任何机器学习或类似的算法活动中使用从必应拼写检查或必应自动推荐 API 接收的数据。

- 为了训练、评估或改进你或者第三方可能会提供的新服务或现有服务，而在任何机器学习或类似的算法活动中使用从必应拼写检查或必应自动推荐 API 接收的数据。

## <a name="2--bing-web-search-image-search-news-search-and-video-search-apis-the-search-apis"></a>2.必应 Web 搜索、图片搜索、新闻搜索和视频搜索 API（统称“搜索 API”）：

**定义。** 以下定义适用于这些使用和显示要求的第 2-7 部分：

- “答复”是指在响应中返回的一类结果。 例如，从必应 Web 搜索 API 返回的响应可能包括网页结果、图片、视频和新闻类别的答复；
- “响应”是指在响应针对搜索 API 的单个调用时收到的任何答复和关联的数据；
- “结果”是指答复中的某项信息。  例如，与单篇新闻文章关联的数据集是新闻答复中的结果。

**Internet 搜索体验。** 在响应中返回的所有数据只能用于 Internet 搜索体验。 Internet 搜索体验是指在适用情况下，所显示的内容符合以下条件：

- 与最终用户的直接查询（或其他表明该用户搜索兴趣和意图的方式，例如用户指示的搜索查询）相关，或者是对其做出的响应； 

- 帮助用户找到和导航到数据源（例如，提供的 URL 以超链接形式实现，使内容或归属成为可单击的链接，与数据一起进行明确显示）； 

- 包含多个可供最终用户选择的结果（例如，显示多个源自新闻答复的结果，或者在返回的结果数不多的情况下显示所有结果）； 

- 根据搜索目的进行尺寸或数量方面的相应限制（例如，缩略图会根据用户的显示屏按比例调整图片大小）； 

- 包含针对最终用户的可见指示，指出内容为 Internet 搜索结果（例如，通过声明指出内容“来自 Web”）；且

- 包含任何其他适当的措施组合，确保你在使用从搜索 API 收到的数据时不违反任何适用的法律或第三方权利。  请咨询你的法律顾问，确定适当的具体措施。

就 Internet 搜索体验要求来说，唯一例外是 URL 发现，详见下面的第 7 部分（非显示 URL 发现）。

**通则。** 你不得： 

- 复制、存储或缓存响应中的任何数据（根据下面的“服务连续性”部分的要求保留这些数据除外）； 

- 修改结果的内容（通过某种方式重新设置其格式除外，但不得违反任何其他要求）； 

- 省略与结果内容关联的归属和 URL；

- 在提供排序功能的情况下，对答复中显示的结果重新排序（包括通过省略的方式重新排序）；

- 在显示某个响应任意部分的其他内容时，所采用的方式会导致最终用户认为这些其他的内容是该响应的一部分； 

- 在任何显示某部分响应的页面上显示不是由 Microsoft 提供的广告；

- 为了训练、评估或改进你或者第三方可能会提供的新服务或现有服务，而在任何机器学习或类似的算法活动中使用从搜索 API 接收的数据。

## <a name="3-advertising"></a>3.广告。
广告（不管是 Microsoft 提供的，还是其他提供商提供的）不得与下述响应一起显示：(i) 由图片、新闻或视频搜索 API 提供的响应：或 (ii) 已经经过筛选或限制的响应，主要（或完全）针对其他搜索 API 提供的图片、新闻和/或视频结果。

## <a name="4-branding"></a>4.品牌。
你需要根据 https://go.microsoft.com/fwlink/?linkid=833278 中的说明，将显示的每个响应（或部分响应）归属于 Microsoft，除非 Microsoft 以书面方式专门针对你的使用进行了约定。


## <a name="5--transferring-responses"></a>5.传输响应。
如果你允许用户通过某种方式将响应传输给其他用户（例如通过消息应用进行传送，或者通过社交媒体进行发布），则应遵守以下准则：

* 传输的响应必须符合以下条件：
  * 包含的内容未经修改，与显示给传输用户的响应内容一致（允许对所做更改进行格式处理）；
  * 不含任何元数据形式的数据；
  * 显示特定的语言文字，指出该响应是通过必应所支持的 Internet 搜索体验获得的（例如，“由必应提供支持”、“请在必应上了解此图片的详细信息”、“请在必应上浏览此图片的详细信息”，或者使用必应徽标）；
  * 突出显示用于生成响应的完整查询；且
  * 包含一个突出显示的指向响应基础源的链接，或者进行类似的归属表示，不管是通过直接方式还是通过 bing.com 或 m.bing.com 这样的间接方式。

* 不得自动传输响应。  传输必须通过用户操作来启动，而且用户操作必须清楚地表明进行响应传输的意图。
* 只能允许用户传输那些通过传输其查询获得的响应。

##<a name="6-continuity-of-service"></a>6.服务连续性。
不得复制、存储或缓存响应中的任何数据。 但是，为了实现服务访问和数据呈现的连续性，可以保留结果，但必须符合以下条件：

**设备。**  可以允许最终用户在设备上保留结果，保留时间为 (i) 查询之后的 24 小时，或者 (ii) 保留到最终用户提交针对已更新结果的另一查询为止，具体取决于二者中哪一个的时间更短，而且保留的结果只能用于以下目的：

- 让最终用户在特定条件下（例如服务中断时）在该设备上访问以前返回给该最终用户的结果；或

- 在根据最终用户的信号预期到该最终用户的需求的情况下（例如，预期服务会中断），存储针对个性化主动查询返回的结果。

**服务器。**  你只能针对以下目的，在所控制的服务器上安全地保留特定于单个最终用户的结果，并且显示保留的结果：

- 让最终用户访问解决方案中此前返回给该用户的结果的历史记录报告，前提是这些结果不得：(i) 超过 21 天的保留时间（从该最终用户的初次查询算起）；(ii) 针对某个最终用户的新查询或重复查询进行响应性显示；或

- 在根据最终用户的信号预期到该最终用户的需求的情况下，存储针对个性化主动查询返回的结果，存储时间为 (i) 查询之后的 24 小时，或者 (ii) 存储到最终用户提交针对已更新结果的另一查询为止，具体取决于二者中哪一个的时间更短。

特定用户的保留结果不能与其他用户的保留结果混合，也就是说，每个用户的结果必须分开保留和交付。

**通则。** 每次呈现保留的结果时，必须符合以下要求：

- 包含清晰可见的标注，注明查询的发送时间；

- 为用户提供按钮或类似按钮的操作方式，方便其再次查询并获取更新的结果； 

- 在呈现结果时保留必应品牌；且

- 在指定的时限内删除存储的结果（以及根据需要使用新查询对其进行刷新）。


##<a name="7--non-display-url-discovery"></a>7.非显示 URL 发现。
你只能在非 Internet 搜索体验中使用搜索响应，且用途仅限于在针对用户或客户的查询进行响应时，发现相关信息源的 URL。 你可以在所提供的报告或类似报告的响应中复制此类 URL，但该报告或响应必须符合以下条件：(i) 只能提供给该用户或客户，作为对特定查询的相应；(ii) 包含与查询相关的重要附加内容。 在上述使用和显示要求中，第 2-6 部分的要求不适用于此非显示使用情形，但以下条款仍适用： 

* 不得缓存、复制或存储任何源自或派生自搜索响应的数据或内容，上述对 URL 进行有限制复制的情形除外；
* 必须确保在使用从搜索 API 收到的数据（包括 URL）时不违反任何适用的法律或第三方权利；且
* 不得为了创建、训练、评估或改进你或者第三方可能会提供的服务，而在任何搜索索引、机器学习或类似的算法活动中使用从搜索 API 接收的数据（包括 URL）。