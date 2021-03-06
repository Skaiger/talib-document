##MACD

【释义】
指数平滑异同移动平均线MACD，是从双移动平均线发展而来的，由快的移动平均线减去慢的移动平均线。当MACD从负数转向正数，是买的信号。当MACD从正数转向负数，是卖的信号。当MACD以大角度变化，表示快的移动平均线和慢的移动平均线的差距非常迅速的拉开，代表了一个市场大趋势的转变。
【算法】
DIF线（Difference）短期移动平均线和长期移动平均线的离差值；
DIF=EMA(q)-EMA(p)
EMA(n)=前一日EMA(n)*(n-1)/(n+1)+C*2/(n+1)
DEA线（Difference Exponential Average）DIF线的M日指数平滑移动平均线 ；
DEA=前一日DEA*（t-1）/(t+1)+DIF*2/(t+1)
MACD线：DIF线与DEA线的差
MACD=DIF-DEA
【函数】
		MACD(...)
MACD(real[, fastperiod=?, slowperiod=?, signalperiod=?])
输入
real: (any ndarray)
参数
fastperiod: 12
slowperiod: 26
signalperiod: 9
输出
macd
macdsignal
macdhist

##AMA

【释义】
	AMA线是指短期移动平均线，它是移动平均线的一种，短期移动平均线是指按照移动时间区限较短这个原则而设定的和计算出来的一种移动平均线。
【算法】
AMA=DMA短期平均值
DMA(n)=n日平均值-m日平均值
AMA(n)=n日DMA平均值
【函数】
	Talib中为WMA
	WMA(real[, timeperiod=?])
输入
real: (any ndarray)
参数
时间周期:30
输出：real


TRIX

【释义】
	该指标是一种三重指数平滑平均线，长线操作时采用本指标的讯号，可以过滤掉一些短期波动的干扰，避免交易次数过于频繁，造成部分无利润的买卖，及手续费的损失，但该指标在盘整行情中不适用。TRIX指标波动频率较低，一年到头出现讯号的机率不多，是一项超长周期的指标，长时间按照本指标讯号交易，获利百分比大于损失百分比，特别是打算进行长期控盘或投资时，利润相当可观。
研判分析主要依赖于TRIX线与TRMA线的交叉情况。

【算法】
TR=收盘价的N日指数移动平均
TRIX=（(TR-昨日TR)/昨日TR）*100
【函数】
TRIX(real[, timeperiod=?])
输入
real: (any ndarray)
参数
timeperiod:30
输出：real

VHF

【释义】
	VHF指标,英文全称Vertical Horizontal Filter,中文名为十字过滤线指标,属于趋势型指标。与常用的MACD、RSI、KDJ等指标不同的是,该指标并不是用来提示超买还是超卖、强势还是弱势,而是用于判断目前的行情是盘整市还是单边市,提示投资者应该采取追涨杀跌还是高抛低吸的操作手法,对投资者在不同市场阶段选择激进还是保守的策略很有帮助
【算法】
	VHF=(HIGH(n)-LOW(n))/SUM(ABS(CLOSE-前一日CLOSE),n)
【函数】
	无

RVI

【释义】
	相对活力指数指标（RVI），是一种通过计算交易日内收盘价、开盘价、最高价、最低价的关系来反映股价趋势的摆荡类技术指标。
【算法】
	RVI=（当日收盘价-当日开盘价）/（当日最高价-当日最低价）
【函数】
	无

KDJ

【释义】
	随机指标是由乔治·莱恩首创的，它在通过当日或最近几日最高价、最低价及收盘价等价格波动的波幅，反映价格趋势的强弱。KDJ一般是用于股票分析的统计体系，根据统计学的原理，通过一个特定的周期（常为9日、9周等）内出现过的最高价、最低价及最后一个计算周期的收盘价及这三者之间的比例关系，来计算最后一个计算周期的未成熟随机值RSV，然后根据平滑移动平均线的方法来计算K值、D值与J值，并绘成曲线图来研判股票走势。
【算法】
N日RSV=(N日收盘价-N日内最低价)÷(N日内最高价-N日内最低价)×100 　
当日K值 = 2/3前1日K值 + 1/3当日RSV；　　
当日D值 = 2/3前1日D值 + 1/3当日K值； 　　
当日J值 = 3当日K值 - 2当日D值。 　　
若无前一日K 值与D值，则可分别用50来代替。
【函数】
	无

BIAS

【释义】
	乖离率也称为Y值，是用股价指数与移动平均线的比值关系，来描述股票价格与移动平均线之间的偏离程度。正乖离率值越大，说明股价向上偏离移动平均线的程度越大，有可能回档下调；反之负乖离值越小，表明股价向下偏离移动平均线的程度越大，随时可能反弹。
【算法】
	BIAS(n)=（当日股市收盘价－n日移动平均值）÷n日移动平均值
【函数】
	无

ForceIndex

【释义】
	强力指数指标（Force Index）由Alexander Elder发明，该技术指标用来指示上升或下降趋势的力量大小，在零线上下移动来表示趋势的强弱。
【算法】
    FORCE INDEX（i）=VOLUME（i）*[MA（ApPRICE，N，i）-MA（ApPRICE，N，i-1）]
　　FORCE INDEX（i）：当前柱的力量指数；
　　VOLUME（i）：当前柱的交易量；
　　MA（ApPRICE，N，i）：在任何一个时段内当前柱的任何移动平均线
　　ApPRICE：应用的价格；
　　N：顺畅的时段；
　　MA（ApPRICE，N，i-1）：前一柱的任何移动平均线。

【函数】
	无

VR

【释义】
	成交量比率（Volume Ratio简称VR）），是一项通过分析股价上升日成交额（或成交量，下同）与股价下降日成交额比值，从而掌握市场买卖气势的中期技术指标。主要用于个股分析，其理论基础是“量价同步”及“量须先于价”，以成交量的变化确认低价和高价，从而确定买卖时法。
【算法】
	VR(n)=SUM(上升日交易量,n)/SUM(下降日交易量,n)
【函数】
	无

DPO

【释义】
	区间震荡线（DPO），是由惠特曼·巴塞特(Walt Bressert)提出的。是一个排除价格趋势的震荡指标。它试图通过扣除前期移动平均价来消除长期趋势对价格波动的干扰，从而便于发现价格短期的波动和超买超卖水平。
【算法】
	DPO=收盘价-前(n/2+1)日MA(n)
【函数】
	手册中有个APO指标（绝对价格震荡指数），不知道是不是这个，百度也找不到二者的区别
APO(real[, fastperiod=?, slowperiod=?, matype=?]))
输入：
	real:(any ndarray)
参数：
	Fastperiod:12
	Slowperiod:26
	Matype:0(simple moving average)
输出：real

NVI

【释义】
负成交量指标又称为负量指标，其作用与正量指标相类似，主要用途除了被利用于寻找买卖点之外，更是侦测大多头市场的主要分析工具
PVI指标的理论观点认为，当日的市况如果价跌量缩时，表示大户主导市场。也就是说，PVI指标主要的功能，在于侦测行情是否属于大户市场。
【算法】
	如果今日成交量大于昨日成交量：
	NVI=前一日NVI
	如果今日成交量小于昨日成交量：
	NVI=前一日NVI*(1+(CLOSE-前一日CLOSE)/前一日CLOSE)
【函数】
	无

PVI

【释义】
	正成交量指标（Positive Volume Index，PVI），PVI指标的理论观点认为，当日的市况如果量增价涨时，表示散户主导市场。相反的，如果当日的成交值缩减，表示精明大户正不动声色的收购股票。也就是说，PVI指标主要的功能，在于侦测行情是否属于散户市场。
【算法】
	PVI(n)=PVI(n-1)*PV(n)；当VOL(n)>VOL(n-1)时，PV(n)=Close(n)/Close(n-1)，否则PV(n)为1
	第一次计算时，PVI一律以100代替; 参数N设置为72
【函数】
	无

ROC

【释义】
	该指标用来测量价位动量，可以同时监视常态性和极端性两种行情。ROC以0为中轴线，可以上升至正无限大，也可以下跌至负无限小。以0轴到第一条超买或超卖线的距离，往上和往下拉一倍、两倍的距离，再画出第二条、第三条超买超卖线，则图形上就会出现上下各三条的天地线。
【算法】
	ROC＝{(当日收盘价－N天前的收盘价)÷N天前的收盘价}*100%
【函数】
	ROC(real[, timeperiod=?])
	输入
real: (any ndarray)
参数
时间周期:10
输出：real

OBV

【释义】
	OBV的英文全称是：On Balance Volume。该指标通过统计成交量变动的趋势来推测股价趋势。OBV以“N”字型为波动单位，并且由许许多多“N”型波构成了OBV的曲线图，对一浪高于一浪的“N”型波，称其为“上升潮”（UP TIDE），至于上升潮中的下跌回落则称为“跌潮”（DOWN FIELD）。
能量潮是将成交量数量化，制成趋势线，配合股价趋势线，从价格的变动及成交量的增减关系，推测市场气氛。其主要理论基础是市场价格的变化必须有成交量的配合，股价的波动与成交量的扩大或萎缩有密切的关连。通常股价上升所需的成交量总是较大；下跌时，则成交量可能放大，也可能较小。价格升降而成交量不相应升降，则市场价格的变动难以为继
【算法】
	当日OBV=前OBV +(-)本日成交量
【函数】
	OBV(real, volume)
	输入
real: (any ndarray)
prices: ['volume']
输出：real

PSY

【释义】
心理线（PSY）指标是研究投资者对股市涨跌产生心理波动的情绪指标。它对股市短期走势的研判具有一定的参考意义。心理线指标将一定时期内投资者趋向买方或卖方的心理事实转化为数值，从而判断股价的未来趋势
【算法】
PSY=N日内上涨天数/N*100
参数N设置为12日
【函数】
	无

MTM

【释义】
	MTM指标又叫动量指标，其英文全称是“Momentum Index”，是一种专门研究股价波动的中短期技术分析工具。它认为股价的涨跌幅度随着时间的推移会逐渐变小，股价变化的速度和能量也会慢慢减缓后，行情就可能反转。在多头行情里，随着股价的不断上升，股价上涨的能量和速度必将日渐萎缩，当上涨的能量和速度减少到一定程度时，行情将会出现大幅回荡整理或见顶反转的行情；而在空头行情里，随着股价地不断下跌，股价下跌的能量和速度也将日渐萎缩，当下跌的能量和速度萎缩到一定程度时，行情也会出现大幅反弹或见底反转的行情。
【算法】
	MTM=当日收盘价-N日前收盘价；
【函数】
	手册中没有MTM函数，但有个MOM（动量）函数，百度得知应该是同一指标
	MOM(real[, timeperiod=?])
输入
real: (any ndarray)
参数
时间周期:10
输出：real

CMO

【释义】
钱德动量摆动指标（Chande Momentum Osciliator，简称CMO），与其他动量指标摆动指标如相对强弱指标（RSI）和随机指标（KDJ）不同，钱德动量指标在计算公式的分子中采用上涨日和下跌日的数据。 CMO指标是寻找极度超买和极度超卖的条件
【算法】
	CMO = （Su - Sd) × 100 / (Su + Sd)
其中：Su是今日收盘价与昨日收盘价（上涨日）差值加总。若当日下跌，则增加值为0；Sd是今日收盘价与做日收盘价（下跌日）差值的绝对值加总。若当日上涨，则增加值为0；
【函数】
CMO(real[, timeperiod=?])
输入
real: (any ndarray)
参数
时间周期:14
输出：real

BBI

【释义】
    BBI(BullAndBearIndex),是按照几种不同日数的移动平均线值根据天数加权平均得到的一项技术指标。主要是为了综合考虑不同日数的移动平均线。
    研判规则：股价在高价区域如果以收市价向下跌破BBI线为卖出信号，在低价区域以收市价向上突破BBI线为买入信号。股价在一段时间内保持在BBI线上方表明多方势力占优，可持股；反之，如果股价一直保持在BBI线下方，表明空方势力强劲，不宜介入。

【算法】
BBI＝(均线1＋均线2＋均线3＋均线4)/4，四条均线天数默认为3，6，12，24 ，均线的计算：n日均价=n日收盘价之和/n

【函数】
	无

BullPower

【释义】
	牛市力量：驱动市场价格上升的力量

【算法】
	Bull Power=目前最高价-EMA（收盘价，13）
	目前最高价的定义并没有给出，推测为当日最高价；EMA为指数平滑移动平均线

【函数】
	无

Bear Power

【释义】
	熊市力量：推动市场价格下降的力量

【算法】
	Bear Power=目前最低价-EMA（收盘价，13）
	目前最低价的定义并没有给出，推测为当日最低价；EMA为指数平滑移动平均线

【函数】
	无

PVT

【释义】
	价量趋势(PVT)指标巧妙地把能量变化与价格趋势有机地联系到了一起，从而构成了量价趋势指标。价格上升，PVT指标线下降为卖出信号；价格下跌，PVT指标线上升为买进信号；PVT的用法基本同OBV，但PVT比OBV能更快地反映趋势。

【算法】
	设x＝(今日收盘价—昨日收盘价)／昨日收盘价×当日成交量，那么当日PVT指标值则为从第一个交易日起每日X值的累加。

【函数】
	无


VOL5：五日平均换手率（略）
VOL10：十日平均换手率（略）

Volatility

【释义】
	换手率相对波动率

【算法】
	网上没有这个指标的定义
	我认为可以用n个交易日的换手率的标准差代替

【函数】
	STDDEV(real[, timeperiod=?, nbdev=?])
输入
real: (any ndarray)
参数
时间周期:5
nbdev: 1
输出：real

RSI

【释义】
	相对强弱指数是根据一定时期内上涨和下跌幅度之和的比率制作出的一种技术曲线,能够反映出市场在一定时期内的景气程度。
RSI值将0到100之间分成了从"极弱"、"弱""强"到"极强"四个区域。"强"和"弱"以50作为分界线,但"极弱"和"弱"之间以及"强"和"极强"之间的界限则要随着RSI参数的变化而变化。RSI值如果超过50,表明市场进入强市,可以考虑买入,但是如果继续进入"极强"区,就要考虑物极必反,准备卖出了。同理RSI值在50以下也是如此,如果进入了"极弱"区,则表示超卖,应该伺机买入。

【算法】
	RSI(n)=N日内收盘价上涨数之和的移动平均值÷（N日内收盘价上涨数之和的移动平均值+N日内收盘价下跌数之和的移动平均值）×100

【函数】
RSI(real[, timeperiod=?])
输入
real: (any ndarray)
参数
时间周期:14
输出：real

ASI

【释义】
	振动升降指标(ASI)以开盘、最高、最低、收盘价与前一交易日的各种价格相比较作为计算因子。

【算法】
　　A=当天最高价-前一天收盘价
　　B=当天最低价-前一天收盘价
　　C=当天最高价-前一天最低价
　　D=前一天收盘价-前一天开盘价
　　A、B、C、D皆采用绝对值

　　E=当天收盘价-前一天收盘价
　　F=当天收盘价-当天开盘价
　　G=前一天收盘价-前一天开盘价
　　E、F、G采用其+－差值

　　X＝E＋1／2F＋G。
　　K=比较A、B两数值，选出其中最大值
　　比较A、B、C三数值：
　　若A最大，则R＝A＋ 1／2B＋ 1／4D
　　若B最大，则R＝B＋1／２A十1／4D
　　若C最大，则R= C＋1/4D
　　L＝3
　　SI= 50* X／R * K／L
ASI=累计每日之SI值

【函数】
	无

MA5：5日移动均线（在上一份文档中，略）
MA20：20日移动均线（略）
