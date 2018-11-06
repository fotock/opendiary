# 1 授权认证
接入方式及流程

### 1、概述

采用通用的OAuth2.0开放授权协议，可以让roome在不获取合作方用户名和密码的前提下，访问用户授权的资源，协议规范可以访问OAuth2.0官方网站：https://oauth.net/2/

PS：家居技能及自定义技能Oauth2.0需要配置的项含义一致，不区分家居和自定义技能

### 2、鉴权流程

（1）roome在开发商开放平台或者其他第三方平台注册一个应用，获取到相应的Client id 和Client secret

（2）roome应用向开发商OAuth2.0服务发起一个授权请求

（3）开发商OAuth2.0服务向用户展示一个授权页面，用户可进行登陆授权

（4）用户授权roome客户端应用后，进行回跳到roome 的回调地址上并带上code相关参数

（5）roome回调地址上根据code会去合作方Oauth 的服务上换取 access_token

（6）通过access_token，设备控制时通过该access_token进行访问合作方的服务

### 3、运行流程

OAuth 2.0的运行流程如下图

  <img src="http://img.alicdn.com/top/i1/LB17GsNRVXXXXb.aXXXXXXXXXXX">
  
（A）用户打开客户端以后，客户端要求用户给予授权。

（B）用户同意给予客户端授权。

（C）客户端使用上一步获得的授权，向认证服务器申请令牌。

（D）认证服务器对客户端进行认证以后，确认无误，同意发放令牌。

（E）客户端使用令牌，向资源服务器申请获取资源。

（F）资源服务器确认令牌无误，同意向客户端开放资源。

<img src="http://homi-img.oss-cn-beijing.aliyuncs.com/561301534110592138.png">
## 2 接入服务

<div class="doc-detail-bd" id="bd" data-spm-anchor-id="0.7629140.0.i8.7dbe1780r26ivK">
<h3>一.协议概述</h3> 
<p>协议分为两部分： header 以及 payload</p> 
<p>示例：</p> 
<div><div id="highlighter_585373" class="syntaxhighlighter  java" title="复制代码请双击"><table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">1</div><div class="line number2 index1 alt1">2</div><div class="line number3 index2 alt2">3</div><div class="line number4 index3 alt1">4</div><div class="line number5 index4 alt2">5</div><div class="line number6 index5 alt1">6</div><div class="line number7 index6 alt2">7</div><div class="line number8 index7 alt1">8</div><div class="line number9 index8 alt2">9</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div><div class="line number12 index11 alt1">12</div><div class="line number13 index12 alt2">13</div><div class="line number14 index13 alt1">14</div><div class="line number15 index14 alt2">15</div><div class="line number16 index15 alt1">16</div><div class="line number17 index16 alt2">17</div><div class="line number18 index17 alt1">18</div><div class="line number19 index18 alt2">19</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="java plain">｛</code></div><div class="line number2 index1 alt1"><code class="java spaces">&nbsp;&nbsp;</code><code class="java string">"header"</code><code class="java plain">:{</code></div><div class="line number3 index2 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"namespace"</code><code class="java plain">:</code><code class="java string">"roome.Iot.Device.Control"</code><code class="java plain">,</code></div><div class="line number4 index3 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"TurnOn"</code><code class="java plain">,</code></div><div class="line number5 index4 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"messageId"</code><code class="java plain">:</code><code class="java string">"1bd5d003-31b9-476f-ad03-71d471922820"</code><code class="java plain">,</code></div><div class="line number6 index5 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"payLoadVersion"</code><code class="java plain">:</code><code class="java value">1</code></div><div class="line number7 index6 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">},</code></div><div class="line number8 index7 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java string">"payload"</code><code class="java plain">:{</code></div><div class="line number9 index8 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"accessToken"</code><code class="java plain">:</code><code class="java string">"access token"</code><code class="java plain">,</code></div><div class="line number10 index9 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string" data-spm-anchor-id="0.7629140.0.i4.7dbe1780r26ivK">"deviceId"</code><code class="java plain">:</code><code class="java string">"34234"</code><code class="java plain">,</code></div><div class="line number11 index10 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceType"</code><code class="java plain">:</code><code class="java string">"XXX"</code><code class="java plain">,</code></div><div class="line number12 index11 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"attribute"</code><code class="java plain">:</code><code class="java string">"powerstate"</code><code class="java plain">,</code></div><div class="line number13 index12 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"value"</code><code class="java plain">:</code><code class="java string">"on"</code><code class="java plain">,</code></div><div class="line number14 index13 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extensions"</code><code class="java plain">:{</code></div><div class="line number15 index14 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extension1"</code><code class="java plain">:</code><code class="java string">""</code><code class="java plain">,</code></div><div class="line number16 index15 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extension2"</code><code class="java plain">:</code><code class="java string">""</code></div><div class="line number17 index16 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number18 index17 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number19 index18 alt2"><code class="java spaces">&nbsp;</code><code class="java plain">｝</code></div></div></td></tr></tbody></table></div></div> 
<h3 data-spm-anchor-id="0.7629140.0.i6.7dbe1780r26ivK">1.1 header参数协议</h3> 
<table> 
 <thead> 
  <tr> 
   <th data-spm-anchor-id="0.7629140.0.i0.7dbe1780r26ivK">参数名 </th> 
   <th>参数类型 </th> 
   <th>参数说明 </th> 
   <th data-spm-anchor-id="0.7629140.0.i2.7dbe1780r26ivK">是否必传 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td data-spm-anchor-id="0.7629140.0.i3.7dbe1780r26ivK">namespace </td> 
   <td>String </td> 
   <td>消息命名空间,详见本页1.2 </td> 
   <td data-spm-anchor-id="0.7629140.0.i1.7dbe1780r26ivK">是 </td> 
  </tr> 
  <tr> 
   <td>name </td> 
   <td>String </td> 
   <td>详见本页1.3 </td> 
   <td>是 </td> 
  </tr> 
  <tr> 
   <td>payLoadVersion </td> 
   <td>int </td> 
   <td>payload 的版本,目前版本为 1 </td> 
   <td>是 </td> 
  </tr> 
  <tr> 
   <td>messageId </td> 
   <td>String </td> 
   <td>用于跟踪请求 </td> 
   <td>是 </td> 
  </tr> 
 </tbody> 
</table> 
<h3 data-spm-anchor-id="0.7629140.0.i7.7dbe1780r26ivK">1.2 header协议中的namespace列表</h3> 
<table> 
 <thead> 
  <tr> 
   <th>namespace </th> 
   <th>解释说明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>roome.Iot.Device.Discovery </td> 
   <td>设备发现 </td> 
  </tr> 
  <tr> 
   <td>roome.Iot.Device.Control </td> 
   <td>设备控制 </td> 
  </tr> 
  <tr> 
   <td>roome.Iot.Device.Query </td> 
   <td>设备属性查询 </td> 
  </tr> 
 </tbody> 
</table> 
<h3>1.3 header协议中name列表</h3> 
<p>1.3.1 设备发现类（与roome.Iot.Device.Discovery对应）</p> 
<table> 
 <thead> 
  <tr> 
   <th>name </th> 
   <th>解释说明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>DiscoveryDevices </td> 
   <td>设备发现（获取设备列表） </td> 
  </tr> 
 </tbody> 
</table> 
<p>1.3.2 操作类（与roome.Iot.Device.Control对应）</p> 
<table> 
 <thead> 
  <tr> 
   <th>name </th> 
   <th>解释说明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>TurnOn </td> 
   <td>打开 </td> 
  </tr> 
  <tr> 
   <td>TurnOff </td> 
   <td>关闭 </td> 
  </tr> 
  <tr> 
   <td>SelectChannel </td> 
   <td>频道切换 </td> 
  </tr> 
  <tr> 
   <td>AdjustUpChannel </td> 
   <td>频道增加 </td> 
  </tr> 
  <tr> 
   <td>AdjustDownChannel </td> 
   <td>频道减少 </td> 
  </tr> 
  <tr> 
   <td>AdjustUpVolume </td> 
   <td>声音按照步长调大 </td> 
  </tr> 
  <tr> 
   <td>AdjustDownVolume </td> 
   <td>声音按照步长调小 </td> 
  </tr> 
  <tr> 
   <td>SetVolume </td> 
   <td>声音调到某个值 </td> 
  </tr> 
  <tr> 
   <td>SetMute </td> 
   <td>设置静音 </td> 
  </tr> 
  <tr> 
   <td>CancelMute </td> 
   <td>取消静音 </td> 
  </tr> 
  <tr> 
   <td>Play </td> 
   <td>播放 </td> 
  </tr> 
  <tr> 
   <td>Pause </td> 
   <td>暂停 </td> 
  </tr> 
  <tr> 
   <td>Continue </td> 
   <td>继续 </td> 
  </tr> 
  <tr> 
   <td>Next </td> 
   <td>下一首或下一台 </td> 
  </tr> 
  <tr> 
   <td>Previous </td> 
   <td>上一首或上一台 </td> 
  </tr> 
  <tr> 
   <td>SetBrightness </td> 
   <td>设置亮度 </td> 
  </tr> 
  <tr> 
   <td>AdjustUpBrightness </td> 
   <td>调大亮度 </td> 
  </tr> 
  <tr> 
   <td>AdjustDownBrightness </td> 
   <td>调小亮度 </td> 
  </tr> 
  <tr> 
   <td>SetTemperature </td> 
   <td>设置温度 </td> 
  </tr> 
  <tr> 
   <td>AdjustUpTemperature </td> 
   <td>调高温度 </td> 
  </tr> 
  <tr> 
   <td>AdjustDownTemperature </td> 
   <td>调低温度 </td> 
  </tr> 
  <tr> 
   <td>SetWindSpeed </td> 
   <td>设置风速 </td> 
  </tr> 
  <tr> 
   <td>AdjustUpWindSpeed </td> 
   <td>调大风速 </td> 
  </tr> 
  <tr> 
   <td>AdjustDownWindSpeed </td> 
   <td>调小风速 </td> 
  </tr> 
  <tr> 
   <td>SetMode </td> 
   <td>模式的切换 </td> 
  </tr> 
  <tr> 
   <td>SetColor </td> 
   <td>设置颜色 </td> 
  </tr> 
  <tr> 
   <td>OpenFunction </td> 
   <td>打开功能 </td> 
  </tr> 
  <tr> 
   <td>CloseFunction </td> 
   <td>关闭功能 </td> 
  </tr> 
  <tr> 
   <td>Cancel </td> 
   <td>取消 </td> 
  </tr> 
  <tr> 
   <td>CancelMode </td> 
   <td>取消模式(退出模式) </td> 
  </tr> 
 </tbody> 
</table> 
<p>1.3.3 查询类（与roome.Iot.Device.Query对应）</p> 
<table> 
 <thead> 
  <tr> 
   <th>支持的查询属性方法 </th> 
   <th>操作方法说明 </th> 
   <th>返回值说明 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>Query </td> 
   <td>查询所有标准属性 </td> 
   <td>详情见各个属性 </td> 
  </tr> 
  <tr> 
   <td>QueryColor </td> 
   <td>查询颜色 </td> 
   <td>Red、Yellow、Blue、White、Black等值（roome以这些值为准，厂家适配） </td> 
  </tr> 
  <tr> 
   <td>QueryPowerState </td> 
   <td>查询电源开关 </td> 
   <td>on(打开)、off(关闭) </td> 
  </tr> 
  <tr> 
   <td>QueryTemperature </td> 
   <td>查询温度 </td> 
   <td>返回数值(roome默认的单位为摄氏度，厂家适配该单位) </td> 
  </tr> 
  <tr> 
   <td>QueryHumidity </td> 
   <td>查询湿度 </td> 
   <td>返回数值 </td> 
  </tr> 
  <tr> 
   <td>QueryWindSpeed </td> 
   <td>查询风速 </td> 
   <td>返回值参考 设备控制 中章节 1.8.1 风速值对应表 </td> 
  </tr> 
  <tr> 
   <td>QueryBrightness </td> 
   <td>查询亮度 </td> 
   <td>返回数值 </td> 
  </tr> 
  <tr> 
   <td>QueryFog </td> 
   <td>查询雾量 </td> 
   <td>返回数值 </td> 
  </tr> 
  <tr> 
   <td>QueryMode </td> 
   <td>查询模式 </td> 
   <td>返回值枚举参考例子模式切换中的例子 </td> 
  </tr> 
  <tr> 
   <td>QueryPM25 </td> 
   <td>查询pm2.5 含量 </td> 
   <td>返回数值 </td> 
  </tr> 
  <tr> 
   <td>QueryDirection </td> 
   <td>查询方向 </td> 
   <td>返回 left,right,forward,back,up,down </td> 
  </tr> 
  <tr> 
   <td>QueryAngle </td> 
   <td>查询角度 </td> 
   <td>返回数值，单位度 </td> 
  </tr> 
 </tbody> 
</table> 
<h3>1.4 payload参数协议</h3> 
<p>payload根据namespace不同分为Discovery、Control、Query三类，详见设备发现、设备控制和设备状态查询。</p>
### 设备发现
<div><div id="highlighter_699786" class="syntaxhighlighter  java" title="复制代码请双击"><table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">1</div><div class="line number2 index1 alt1">2</div><div class="line number3 index2 alt2">3</div><div class="line number4 index3 alt1">4</div><div class="line number5 index4 alt2">5</div><div class="line number6 index5 alt1">6</div><div class="line number7 index6 alt2">7</div><div class="line number8 index7 alt1">8</div><div class="line number9 index8 alt2">9</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="java plain">{</code></div><div class="line number2 index1 alt1"><code class="java spaces">&nbsp;&nbsp;</code><code class="java string">"header"</code><code class="java plain">:{</code></div><div class="line number3 index2 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"namespace"</code><code class="java plain">:</code><code class="java string">"roome.Iot.Device.Discovery"</code><code class="java plain">,</code></div><div class="line number4 index3 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"DiscoveryDevices"</code><code class="java plain">,</code></div><div class="line number5 index4 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"messageId"</code><code class="java plain">:</code><code class="java string" data-spm-anchor-id="0.7629140.0.i2.4d2d1780El68Fj">"1bd5d003-31b9-476f-ad03-71d471922820"</code><code class="java plain">,</code></div><div class="line number6 index5 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"payLoadVersion"</code><code class="java plain">:</code><code class="java value">1</code></div><div class="line number7 index6 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">},</code></div><div class="line number8 index7 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java string">"payload"</code><code class="java plain">:{</code></div><div class="line number9 index8 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"accessToken"</code><code class="java plain">:</code><code class="java string">"access token"</code></div><div class="line number10 index9 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">｝</code></div><div class="line number11 index10 alt2"><code class="java spaces">&nbsp;&nbsp;</code><code class="java plain">}</code></div></div></td></tr></tbody></table></div></div>
<h4>响应</h4>
<table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">1</div><div class="line number2 index1 alt1">2</div><div class="line number3 index2 alt2">3</div><div class="line number4 index3 alt1">4</div><div class="line number5 index4 alt2">5</div><div class="line number6 index5 alt1">6</div><div class="line number7 index6 alt2">7</div><div class="line number8 index7 alt1">8</div><div class="line number9 index8 alt2">9</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div><div class="line number12 index11 alt1">12</div><div class="line number13 index12 alt2">13</div><div class="line number14 index13 alt1">14</div><div class="line number15 index14 alt2">15</div><div class="line number16 index15 alt1">16</div><div class="line number17 index16 alt2">17</div><div class="line number18 index17 alt1">18</div><div class="line number19 index18 alt2">19</div><div class="line number20 index19 alt1">20</div><div class="line number21 index20 alt2">21</div><div class="line number22 index21 alt1">22</div><div class="line number23 index22 alt2">23</div><div class="line number24 index23 alt1">24</div><div class="line number25 index24 alt2">25</div><div class="line number26 index25 alt1">26</div><div class="line number27 index26 alt2">27</div><div class="line number28 index27 alt1">28</div><div class="line number29 index28 alt2">29</div><div class="line number30 index29 alt1">30</div><div class="line number31 index30 alt2">31</div><div class="line number32 index31 alt1">32</div><div class="line number33 index32 alt2">33</div><div class="line number34 index33 alt1">34</div><div class="line number35 index34 alt2">35</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="java plain">{</code></div><div class="line number2 index1 alt1"><code class="java spaces">&nbsp;&nbsp;</code><code class="java string">"header"</code><code class="java plain">:{</code></div><div class="line number3 index2 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"namespace"</code><code class="java plain">:</code><code class="java string">"roome.Iot.Device.Discovery"</code><code class="java plain">,</code></div><div class="line number4 index3 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"DiscoveryDevicesResponse"</code><code class="java plain">,</code></div><div class="line number5 index4 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"messageId"</code><code class="java plain">:</code><code class="java string">"1bd5d003-31b9-476f-ad03-71d471922820"</code><code class="java plain">,</code></div><div class="line number6 index5 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"payLoadVersion"</code><code class="java plain">:</code><code class="java value">1</code></div><div class="line number7 index6 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">},</code></div><div class="line number8 index7 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java string">"payload"</code><code class="java plain">:{</code></div><div class="line number9 index8 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"devices"</code><code class="java plain">:[{</code></div><div class="line number10 index9 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceId"</code><code class="java plain">:</code><code class="java string">"34ea34cf2e63"</code><code class="java plain">,</code></div><div class="line number11 index10 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceName"</code><code class="java plain">:</code><code class="java string">"light1"</code><code class="java plain">,</code></div><div class="line number12 index11 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceType"</code><code class="java plain">:</code><code class="java string">"light"</code><code class="java plain">,</code></div><div class="line number13 index12 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"zone"</code><code class="java plain">:</code><code class="java string">""</code><code class="java plain">,&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </code></div><div class="line number14 index13 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"brand"</code><code class="java plain">:</code><code class="java string">""</code><code class="java plain">,</code></div><div class="line number15 index14 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"model"</code><code class="java plain">:</code><code class="java string">""</code><code class="java plain">,&nbsp;&nbsp;&nbsp;&nbsp; </code></div><div class="line number16 index15 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"icon"</code><code class="java plain">:</code><code class="java string">"<a href="  ">  </a>"</code><code class="java plain">,</code></div><div class="line number17 index16 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"properties"</code><code class="java plain">:[{</code></div><div class="line number18 index17 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"color"</code><code class="java plain">,</code></div><div class="line number19 index18 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"value"</code><code class="java plain">:</code><code class="java string">"Red"</code></div><div class="line number20 index19 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}],</code></div><div class="line number21 index20 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"actions"</code><code class="java plain">:[</code></div><div class="line number22 index21 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"TurnOn"</code><code class="java plain">,</code></div><div class="line number23 index22 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"TurnOff"</code><code class="java plain">,</code></div><div class="line number24 index23 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"SetBrightness"</code><code class="java plain">,&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </code></div><div class="line number25 index24 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"AdjustBrightness"</code><code class="java plain">,&nbsp;&nbsp;&nbsp;&nbsp; </code></div><div class="line number26 index25 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"SetTemperature"</code><code class="java plain">,</code></div><div class="line number27 index26 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"Query"</code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</div><div class="line number28 index27 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">],</code></div><div class="line number29 index28 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extensions"</code><code class="java plain">:{</code></div><div class="line number30 index29 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extension1"</code><code class="java plain">:</code><code class="java string">""</code><code class="java plain">,</code></div><div class="line number31 index30 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extension2"</code><code class="java plain">:</code><code class="java string">""</code></div><div class="line number32 index31 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number33 index32 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}]</code></div><div class="line number34 index33 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number35 index34 alt2"><code class="java plain">}</code></div></div></td></tr></tbody></table>
<p>payload 协议参数说明：</p>
<table> 
 <thead> 
  <tr> 
   <th>参数名 </th> 
   <th>参数类型 </th> 
   <th>参数说明</th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>devices </td> 
   <td>JSON Object List </td> 
   <td>用户设备列表</td> 
  </tr> 
 </tbody> 
</table>
<p>JSON Object 对象说明</p>
<table> 
 <thead> 
  <tr> 
   <th>参数名 </th> 
   <th>参数类型 </th> 
   <th>参数说明 </th> 
   <th>返回值是否允许为空 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>deviceId </td> 
   <td>String </td> 
   <td>设备Id </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>deviceType </td> 
   <td>String </td> 
   <td>设备类型,具体参考roome支持的品类列表 </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>deviceName </td> 
   <td>String </td> 
   <td>名称 </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>brand </td> 
   <td>String </td> 
   <td>品牌 </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>model </td> 
   <td>String </td> 
   <td>型号 </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>zone </td> 
   <td>String </td> 
   <td>位置 </td> 
   <td>可选 </td> 
  </tr> 
  <tr> 
   <td>icon </td> 
   <td>String </td> 
   <td>产品icon(https协议的url链接),像素最好160*160 以免在app显示模糊 </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>properties </td> 
   <td>JSON List </td> 
   <td>返回当前设备支持的属性状态列表，产品支持的属性列表参考 设备控制与设备状态查询页 的 第二部分 设备状态查询 2.2 章节 </td> 
   <td>否 </td> 
  </tr> 
  <tr> 
   <td>actions </td> 
   <td>List 
    <string> 
    </string></td> 
   <td>产品支持的操作(注：包括支持的查询操作) ,详情参照 协议简介 中 1.3.2和1.3.3章节 </td> 
   <td>否(万能遥控器除外) </td> 
  </tr> 
  <tr> 
   <td>extensions </td> 
   <td>Object </td> 
   <td>产品扩展属性,为空返回null或者不返回该字段 </td> 
   <td>可选 </td> 
  </tr> 
 </tbody> 
</table>
#### 设备控制
示例
<p>设备打开</p>
<div id="highlighter_776863" class="syntaxhighlighter  java  " title="复制代码请双击"><table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">1</div><div class="line number2 index1 alt1">2</div><div class="line number3 index2 alt2">3</div><div class="line number4 index3 alt1">4</div><div class="line number5 index4 alt2">5</div><div class="line number6 index5 alt1">6</div><div class="line number7 index6 alt2">7</div><div class="line number8 index7 alt1">8</div><div class="line number9 index8 alt2">9</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div><div class="line number12 index11 alt1">12</div><div class="line number13 index12 alt2">13</div><div class="line number14 index13 alt1">14</div><div class="line number15 index14 alt2">15</div><div class="line number16 index15 alt1">16</div><div class="line number17 index16 alt2">17</div><div class="line number18 index17 alt1">18</div><div class="line number19 index18 alt2">19</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="java plain" data-spm-anchor-id="0.7629140.0.i2.7d341780ixvY1Q">｛</code></div><div class="line number2 index1 alt1"><code class="java spaces">&nbsp;&nbsp;</code><code class="java string">"header"</code><code class="java plain">:{</code></div><div class="line number3 index2 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"namespace"</code><code class="java plain">:</code><code class="java string" data-spm-anchor-id="0.7629140.0.i3.7d341780ixvY1Q">"roome.Iot.Device.Control"</code><code class="java plain">,</code></div><div class="line number4 index3 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"TurnOn"</code><code class="java plain">,</code></div><div class="line number5 index4 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"messageId"</code><code class="java plain">:</code><code class="java string">"1bd5d003-31b9-476f-ad03-71d471922820"</code><code class="java plain">,</code></div><div class="line number6 index5 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"payLoadVersion"</code><code class="java plain">:</code><code class="java value">1</code></div><div class="line number7 index6 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">},</code></div><div class="line number8 index7 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java string">"payload"</code><code class="java plain">:{</code></div><div class="line number9 index8 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"accessToken"</code><code class="java plain">:</code><code class="java string">"access token"</code><code class="java plain">,</code></div><div class="line number10 index9 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceId"</code><code class="java plain">:</code><code class="java string">"34234"</code><code class="java plain">,</code></div><div class="line number11 index10 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceType"</code><code class="java plain">:</code><code class="java string">"XXX"</code><code class="java plain">,</code></div><div class="line number12 index11 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"attribute"</code><code class="java plain">:</code><code class="java string">"powerstate"</code><code class="java plain">,</code></div><div class="line number13 index12 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"value"</code><code class="java plain">:</code><code class="java string">"on"</code><code class="java plain">,</code></div><div class="line number14 index13 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extensions"</code><code class="java plain">:{</code></div><div class="line number15 index14 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extension1"</code><code class="java plain">:</code><code class="java string">""</code><code class="java plain">,</code></div><div class="line number16 index15 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"extension2"</code><code class="java plain">:</code><code class="java string">""</code></div><div class="line number17 index16 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number18 index17 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number19 index18 alt2"><code class="java spaces">&nbsp;</code><code class="java plain">｝</code></div></div></td></tr></tbody></table></div>
<p>正常响应</p>
<div><div id="highlighter_922638" class="syntaxhighlighter  java" title="复制代码请双击"><table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">1</div><div class="line number2 index1 alt1">2</div><div class="line number3 index2 alt2">3</div><div class="line number4 index3 alt1">4</div><div class="line number5 index4 alt2">5</div><div class="line number6 index5 alt1">6</div><div class="line number7 index6 alt2">7</div><div class="line number8 index7 alt1">8</div><div class="line number9 index8 alt2">9</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="java plain">｛</code></div><div class="line number2 index1 alt1"><code class="java spaces">&nbsp;&nbsp;</code><code class="java string">"header"</code><code class="java plain">:{</code></div><div class="line number3 index2 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"namespace"</code><code class="java plain">:</code><code class="java string">"roome.Iot.Device.Control"</code><code class="java plain">,</code></div><div class="line number4 index3 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"TurnOnResponse"</code><code class="java plain">,</code></div><div class="line number5 index4 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"messageId"</code><code class="java plain">:</code><code class="java string">"1bd5d003-31b9-476f-ad03-71d471922820"</code><code class="java plain">,</code></div><div class="line number6 index5 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"payLoadVersion"</code><code class="java plain">:</code><code class="java value">1</code></div><div class="line number7 index6 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">},</code></div><div class="line number8 index7 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java string">"payload"</code><code class="java plain">:{</code></div><div class="line number9 index8 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceId"</code><code class="java plain">:</code><code class="java string">"34234"</code></div><div class="line number10 index9 alt1" data-spm-anchor-id="0.7629140.0.i6.7d341780ixvY1Q"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number11 index10 alt2"><code class="java spaces">&nbsp;</code><code class="java plain">｝</code></div></div></td></tr></tbody></table></div></div>
<p>异常响应</p>
<div><div id="highlighter_361237" class="syntaxhighlighter  java" title="复制代码请双击"><table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">1</div><div class="line number2 index1 alt1">2</div><div class="line number3 index2 alt2">3</div><div class="line number4 index3 alt1">4</div><div class="line number5 index4 alt2">5</div><div class="line number6 index5 alt1">6</div><div class="line number7 index6 alt2">7</div><div class="line number8 index7 alt1">8</div><div class="line number9 index8 alt2">9</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div><div class="line number12 index11 alt1">12</div><div class="line number13 index12 alt2">13</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="java plain">｛</code></div><div class="line number2 index1 alt1"><code class="java spaces">&nbsp;&nbsp;</code><code class="java string">"header"</code><code class="java plain">:{</code></div><div class="line number3 index2 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"namespace"</code><code class="java plain">:</code><code class="java string">"roome.Iot.Device.Control"</code><code class="java plain">,</code></div><div class="line number4 index3 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"name"</code><code class="java plain">:</code><code class="java string">"ErrorResponse"</code><code class="java plain">,</code></div><div class="line number5 index4 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"messageId"</code><code class="java plain">:</code><code class="java string">"1bd5d003-31b9-476f-ad03-71d471922820"</code><code class="java plain">,</code></div><div class="line number6 index5 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"payLoadVersion"</code><code class="java plain">:</code><code class="java value">1</code></div><div class="line number7 index6 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java plain">},</code></div><div class="line number8 index7 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;</code><code class="java string">"payload"</code><code class="java plain">:{</code></div><div class="line number9 index8 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"deviceId"</code><code class="java plain">:</code><code class="java string">"34234"</code><code class="java plain">,</code></div><div class="line number10 index9 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"errorCode"</code><code class="java plain">:</code><code class="java string">"DEVICE_NOT_SUPPORT_FUNCTION"</code><code class="java plain">,</code></div><div class="line number11 index10 alt2"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java string">"message"</code><code class="java plain">:</code><code class="java string">"device not support"</code></div><div class="line number12 index11 alt1"><code class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="java plain">}</code></div><div class="line number13 index12 alt2"><code class="java spaces">&nbsp;&nbsp;</code><code class="java plain">｝</code></div></div></td></tr></tbody></table></div></div>
