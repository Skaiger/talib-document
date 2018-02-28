TA-Lib
===========================
TA-Lib是一个优秀的技术指标计算工具包，广泛应用于量化分析和程序化交易，常用语技术指标计算以及K线形态识别，可以大大方便我们量化投资中编程工作。TA-Lib主要包括10大类工具：

****

## Overlap Studies(重叠指标)

## Volume Indicators(交易量指标)

## Cycle Indicators(周期指标)

## Price Transform(价格变换)

## Volatility Indicators(波动率指标)

## Pattern Recognition(模式识别)

## Statistic Functions(统计函数)

## Math Transform(数学变换)

## Math Operators(数学运算)
****

# Overlapping Studies Function(重叠指标)
以均线为代表的重叠指标是最常用的技术指标之一，TALib中提供了很多重叠指标的计算功能，汇总如下：


### Simple Moving Average——简单均线           
代码：SMA(close,timeperiod=N)

简介说明：N日收盘价之和/N，解释价格平均移动最普遍的方法是就是将其动量与价格运动相比较。当价格上升到其移动平均线之上时，则视为一个买入信号；当价格下落到移动平均线下面时，可视为一个卖出信号。均线的含义类似，只是计算方法不同，特别是采用不同的平滑方法之后。


### Exponential Moving Average——指数平滑均线
代码：EMA(close,timeperiod=N)

简介说明：平滑系数*(当日收盘价-昨日计算的N日收盘均值)+昨日计算的N日收盘均值，平滑系数=2/(N+1)



### Weighted Moving Average——加权平滑均线

代码：WMA(close,timeperiod=N)

简介说明：收盘价1*1+收盘价2*2+...+收盘价N*N / (1+2+3+...+N)


### Bollinger Band——布林带
代码：BBANDS(close, timeperiod=5, nbdevup=2, nbdevdn=2, matype=0)     
简介说明：中间线=过去20交易日收盘价均线；Upper线=中间线+2*过去20交易日收盘价的标准差；Down线=中间线-2*过去20交易日收盘价的标准差


### Double Exponential Moving Average——双指数移动平均线           
代码：DEMA(close, timeperiod=30)
简介说明：是一种平滑方法。基于指数移动平均线EMA，与当前价格，存在一个EMA误差(当前价格-价格系列以N为周期的EMA的当前值err(i) = Price(i) - EMA(Price, N, i))，双指数平滑是将该EMA误差也做一次EMA再添加到指数移动平均上，即DEMA(i) = EMA(Price, N, i) + EMA(err, N, i)


### Hilbert Transform - Instantaneous Trendline   ——希尔伯特变换——瞬时趋势线      

代码：HT_TRENDLINE(close)

简介说明：略


### Kaufman Adaptive Moving Average——考夫曼自适应移动平均线

代码：KAMA(close, timeperiod=30)

简介说明：KAMA = KAMA[1] + C*(PRICE – KAMA[1])，其中平滑系数C是自适应的体现，C的计算如下：fastest = 2/(N+1) ，slowest = 2/(N+1) ，smooth = ER*(fastest - slowest) + slowest，c = smooth*smooth，其中ER为效率系数，ER=direction/volatility，direction = price – price[n](当前价格-n天前的收盘价)，volatility=sum(abs(price – price[i]), n)(前n天direction绝对值的和)

自适应均线的提出，是希望当价格沿某一个方向快速移动时，采用合适的短期均线；当价格在横盘中，则用长期的移动均线。


### MESA Adaptive Moving Average       MESA——自适应移动平均

MAMA(close, fastlimit=0, slowlimit=0)

简介说明：略



### Moving average with variable period——变周期移动平均线

MAVP(close, periods, minperiod=2, maxperiod=30, matype=0)

简介说明：略



### MidPoint over period

代码：MIDPOINT(close, timeperiod=14)

简介说明：一段时间收盘价的最大值和最小值的均值构成的线



### Midpoint Price over period

代码：MIDPRICE(high, low, timeperiod=14)   

简介说明：一段时间高价的最大值和低价的最小值的均值构成的线



### Parabolic SAR      抛物线指标

代码：SAR(high, low, acceleration=0, maximum=0) 

简介说明：对于长线交易，SAR (i) = SAR (i - 1) + ACCELERATION * (HIGH (i - 1) - SAR (i - 1))；对于短线交易，SAR (i) = SAR (i - 1) + ACCELERATION * (LOW (i - 1) - SAR (i - 1))，其中SAR (i - 1) 为前一个抛物线转向指标值，ACCELERATION为加速因子，HIGH (i - 1)为前一周期的最高价，LOW (i - 1) 为前一周期的最低价。

抛物线转向技术指标是用来分析市场的趋势变化的，和移动平均线技术指标。唯一的差别就是抛物线转向指标是以越来越快的速度加速移动的，并且就价格而改变自己的位置。该指标在牛市时（上升趋势）低于价格水平，在熊市时（下降趋势）高于价格水平。



### Triple Exponential Moving Average (T3)  三指数移动平均线(T3)

T3(close, timeperiod=5, vfactor=0)

简介说明：和三指数移动平均线类似。



### Triple Exponential Moving Average   三指数移动平均线

代码：TEMA(close, timeperiod=30)   

简介说明：是对于双指数均线DEMA的进一步平滑。err(i) = Price(i) -DEMA(Price, N,i)为DEMA价格偏差，而TEMA(i) = DEMA(Price, N, i) + EMA(err, N, i)



### Triangular Moving Average 三角形加权法

代码：TRIMA(close, timeperiod=30)

简介说明：略



# Momentum Indicator Functions(动量指标)
动量指标是技术分析中最为常用的指标，在TAlib中也提供了很多动量指标计算的函数，汇总如下：



### 指数平滑异同移动平均线(MACD)

代码：ta.MACD(close, fastperiod=6, slowperiod=12, signalperiod=9)

简介说明：MACD的原理是运用短期（快速）和长期（慢速）移动平均线聚合和分散的征兆加以双重平滑运算，用来合理择时。根据移动平均线的特性，在一段持续的涨势中短期移动平均线和长期移动平均线之间的距离将愈拉愈远，两者间的乖离越来越大，涨势如果趋向缓慢，两者间的距离也必然缩小，甚至互相交叉，发出卖出信号。同样，在持续的跌势中，短期线在长期线之下，相互之间的距离越来越远，如果跌势减缓，两者之间的距离也将缩小，最后交叉发出买入信号。

计算方法：差离值DIF = 短期EMA - 中长期EMA；差离平均值DEA = 差离值DIF的N日移动平均值；DIF向上突破DEA时为买进信号；DIF向下跌破DEA时为卖出信号



### 随机指数(Stochastics / KDJ)

代码：STOCH(high, low, close, fastk_period=5, slowk_period=3, slowk_matype=0, slowd_period=3, slowd_matype=0)

简介说明：KDJ指标根据统计学原理，通过一个特定的周期（常为9日、9周等）内出现过的最高价、最低价及最后一个计算周期的收盘价及这三者之间的比例关系，来计算最后一个计算周期的未成熟随机值RSV，然后根据平滑移动平均线的方法来计算K值、D值与J值，并绘成曲线图来研判股票走势。

计算方法：N日RSV = (第N日收盘价-N日内最低价)/(N日内最高价-N日内最低价)*100

第N日K值 = 2/3*N-1日K值 + 1/3*第N日RSV,第N日D值 = 2/3*N-1日D值 + 1/3*第N日K值，第N-1日无K或D值，则可用50代替，第N日J值 = 3*第N日K值 - 2*第N日D值(talib不自动计算J值)



### Average Directional Movement Index——平均方向移动指数

代码：ADX(high, low, close, timeperiod=14)

简介说明：属于震荡指标，指示市场趋势的强弱程度。计算较为繁琐这里不再详述。当ADX指标从20以下上升到20以上，趋势就开始发展，从40以上降到40以下时，趋势就会结束。ADX指标是由+DI，-DI和一条ADX趋势线组成的。建议当+DI指标高于-DI指标时进行买入，在+DI指标下沉到低于-DI指标时卖出



### Average Directional Movement Index Rating——平均方向移动指标排名

代码：ADXR(high, low, close, timeperiod=14)

简介说明：是ADX的平滑结果，为当前ADX和14天前ADX的算术平均



### Absolute Price Oscillator——绝对价格振荡器     

代码：APO(close, fastperiod=12, slowperiod=26, matype=0)

简介说明：为市场强弱指标，返回两个时间序列，第一个是9个时间段和16个时间段的简单移动平均的差异，第二个是一条信号线，表示为第一个的9个时间段的指数平均移动



### Aroon——阿隆指标

代码：AROON(high, low, timeperiod=14)

简介说明：用于帮助预测价格趋势到趋势趋于的变化。计算如下：Aroon(上升)=[(计算期天数-最高价后的天数)/计算期天数]*100；Aroon(下降)=[(计算期天数-最低价后的天数)/计算期天数]*100



### Aroon Oscillator——阿隆振荡器

代码：AROONOSC(high, low, timeperiod=14)

简介说明：Aroon(上升)和Aroon(下降)之间的差值



### Balance Of Power——均势指标

代码：BOP(open, high, low, close)

简介说明：该指标用于反映价格在某一段时间的空间离散率。在盘整中，走势价格被束缚在上下轨道之间；在趋势中，走势价格偏离在均线之下



### Commodity Channel Index——商品通道指数

代码：CCI(high, low, close, timeperiod=14)

简介说明：商品通道指数技术指标（CCI）测量商品价格与其平均统计价格的偏差值。该指数的高值表明，与平均价格相比，价格非常高的。 低值说明价格过于的低了。虽然是这个名字，商品通道指数却可以应用于除了商品以外的任何金融测算工具。CCI的计算流程如下：1.计算典型价格TP = (HIGH + LOW + CLOSE) / 3，2.计算典型价格在n-周期简单移动平均线:

SMA (TP, N) = SUM (TP, N) / N，3.从n周期之前的每个典型价格里扣除已经得到的SMA(TP, N):D = TP - SMA (TP, N)，4.计算绝对值D在n-周期简单移动平均线:SMA (D, N) = SUM (D, N) / N，5.0.015乘以得到的SMA(D, N):M = SMA (D, N) * 0,015，6.用M除以D:CCI = M / D



### Chande Momentum Oscillator——钱德动量摆动指标

代码：CMO(close, timeperiod=14)     

简介说明： CMO=（Su－Sd）*100/（Su+Sd），其中Su是今日收盘价与昨日收盘价（上涨日）差值加总。若当日下跌，则增加值为0；Sd是今日收盘价与做日收盘价（下跌日）差值的绝对值加总。若当日上涨，则增加值为0



### Directional Movement Index——方向性移动指标

代码：DX(high, low, close, timeperiod=14)

简介说明：属于震荡指标，指示市场趋势的强弱程度；平滑后得到ADX



### MACD with controllable MA type     ——带可控MA类型的MACD

代码：MACDEXT(close, fastperiod=12, fastmatype=0, slowperiod=26, slowmatype=0, signalperiod=9, signalmatype=0)

简介说明：MACD的变形



### Moving Average Convergence/Divergence Fix 12/26——移动平均收敛/散度 固定 12/26      

代码：MACDFIX(close, signalperiod=9)

简介说明：MACD的变形



### Money Flow Index——资金流量指标

代码：MFI(high, low, close, volume, timeperiod=14)

简介说明：根据成交量来计测市场供需关系和买卖力道。该指标是通过反映股价变动的四个元素：上涨的天数、下跌的天数、成交量增加幅度、成交量减少幅度来研判量能的趋势，预测市场供求关系和买卖力道，属于量能反趋向指标



### Minus Directional Indicator——负向指标

代码：MINUS_DI(high, low, close, timeperiod=14)

简介说明：略



### Minus Directional Movement——负向运行指标

代码：MINUS_DM(high, low, timeperiod=14)

简介说明：略



### Momentum——动量  

代码：MOM(close, timeperiod=10)

简介说明：当前价格/n周期前的价格*100，CLOSE (i) / CLOSE (i - n) * 100

动量一般有两种用法，其一是作为一种追随市场趋势的指标动量类似MACD。其二是作为引导性指标。



### Plus Directional Indicator——正向指标

代码：PLUS_DI(high, low, close, timeperiod=14)

简介说明：略



### Plus Directional Movement——正向移动指标

代码：PLUS_DM(high, low, timeperiod=14)

简介说明：略

### Percentage Price Oscillator——比例价格振荡器

代码：PPO(close, fastperiod=12, slowperiod=26, matype=0)

简介说明：和MACD类似，但采用百分比数值来说明。其计算为收盘价的12日EMA与26日EMA的差值比26日EMA



### Rate of change——变化率

代码：ROC(close, timeperiod=10)

简介说明：当前价格/前一周期的价格*100，((price/prevPrice)-1)*100



### Rate of change Percentage——变化率百分比

代码：ROCP(close, timeperiod=10)

简介说明：(当前价格-前一周期的价格)/前一周期的价格，(price-prevPrice)/prevPrice



### Rate of change ratio——变化率的比率  

代码：ROCR(close, timeperiod=10)

简介说明：当前价格/前一周期的价格，(price/prevPrice)      



### Rate of change ratio 100 scale——变化率的比率100倍     

代码：ROCR100(close, timeperiod=10)

简介说明：当前价格/前一周期的价格*100，(price/prevPrice)*100



### Relative Strength Index——相对强弱指数    

代码：RSI(close, timeperiod=14)

简介说明：RSI＝[上升平均数÷(上升平均数＋下跌平均数)]×100，其中上升平均数：在某一段日子里升幅数的平均；下跌平均数：在同一段日子里跌幅数的平均。一般的，当RSI高于70时，股票可以被视为超买，是卖出的时候，而当RSI低于30时，股票可以被视为超卖，是买入的时候



### Stochastic Fast——随机指标快速线

代码：STOCHF(high, low, close, fastk_period=5, fastd_period=3, fastd_matype=0)      

简介说明：：计算随机指标KDJ的快速线：Fast K =  [(Close - Low) / (High - Low)] x 100；Fast D = Fast K的SMA (一般周期取3)

Stochastic Relative Strength Index——       随机相对强弱指标      



### Stochastic Relative Strength Index——    随机相对强弱指标    

代码：STOCHRSI(close, timeperiod=14, fastk_period=5, fastd_period=3, fastd_matype=0)

简介说明：是RSI的延伸。其计算为：StochRSI = (RSI - LowRSIn) / (HighRSIn - LowRSIn)，其中RSI为当前RSI值，LowRSIn为过去n期最小的RSI，HighRSIn为过去n期最大的RSI



### 1-day Rate-Of-Change (ROC) of a Triple Smooth EMA——三重光滑EMA的日变化率      

代码：TRIX(close, timeperiod=30)

简介说明：该区域是用作过渡买入或者过渡卖出状态的指标（分别为正负值）。买入信号是从下与零线相交，或者“牛市”分离；卖出信号是从上部与零线相交，或者价格“熊市”分离。TRIX即是三倍指数移动平均线的变化率，TRIX(i) = (EMA3(i) - EMA3(i - 1))/ EMA3(i-1)



### Ultimate Oscillator——终极指标

代码：ULTOSC(high, low, close, timeperiod1=7, timeperiod2=14, timeperiod3=28)

简介说明：先找出三个周期不同的振荡指标，再将这些周期参数，按照反比例的方式，制作成常数因子。然后，依照加权的方式，将三个周期不同的振荡指标，分别乘以不同比例的常数，加以综合制作成UOS指标。其计算流程如下：　1、TH＝MAX（今日最高价，昨日收盘价），2、TL＝MIN（今日最低价，昨日收盘价），3、TR＝TH－TL，4、XR＝当日收盘价－TL，5、XRM＝（M天的XR和÷M天的TR和），6、XRN＝（N天的XR和÷N天的TR和），7、XRO＝（O天的XR和÷0天的TR和），8、UOS＝第5、6、7项参数的反比例值(一般参数M=7，N＝14，O＝28)



### Williams' %R ——威廉指标

代码：WILLR(high, low, close, timeperiod=14)

简介说明：威廉技术指标 (%R)是一个动态技术指标，由它来决定市场是否过度买入/过度卖出。-80%到-100%之间变化的指标值表示市场处于过度卖出状态。-0%到-20%之间变化的指标值表示市场处于过度买入状态。为表明威廉指标的上下运动方式，需要在威廉指标值前加负号（例如-30%）。不过在进行指标分析时，可以忽略那个负号的存在。其计算如下：%R = -(MAX (HIGH (i - n)) - CLOSE (i)) / (MAX (HIGH (i - n)) - MIN (LOW (i - n))) * 100，其中CLOSE (i)为当前收盘价，MAX (HIGH (i - n))为上一周期数(n)的最大最高价，MIN (LOW (i - n))为上一周期数(n)的最小最低价

# Volume Indicator Functions(交易量指标)
交易量指标作为量价指标的一部分，在技术分析往往辅助判断价格的走势(和价格指标一起使用)，在TALib中交易量指标只有3个，汇总如下：

### Chaikin A/D Line——收集派发线          

代码：AD(high, low, close, volume)

简介说明：今日的A/D值 = 昨天的A/D值＋（收盘价位置常数×成交量） 收盘价位置常数=((收盘价－最低价)－(最高价－收盘价))/(最高价－收盘价)


### Chaikin A/D Oscillator——收集派发震荡指标    

代码：ADOSC(high, low, close, volume, fastperiod=3, slowperiod=10)  

简介说明：收集派发线的3日EMA值与10日EMA值的差值


### On Balance Volume——能量潮指标

代码：OBV(close, volume)

简介说明：今日OBV = 昨日OBV+sgn×今天的成交量，sgn是符号函数，sgn=+1 今日收盘价≥昨日收盘价；sgn=-1 今日收盘价<昨日收盘价



# Volatility Indicator Functions(波动性指标)
波动性指标，用于衡量价格的波动情况，辅助判断趋势改变的可能性，市场的交易氛围，也可以利用波动性指标来帮助止损止盈，在TALib中波动性指标只有3个，汇总如下：



### Average True Range——平均真实波动范围

代码：ATR(high, low, close, timeperiod=14)

简介说明：当前交易日的最高价与最低价间的波幅，前一交易日收盘价与当个交易日最高价间的波幅，前一交易日收盘价与当个交易日最低价间的波幅，这三者中的最大值为真实波幅，有了真实波幅后，一段时间的真实波幅平均值就是ATR



### Normalized Average True Range——正态化平均真实波动范围       

代码：NATR(high, low, close, timeperiod=14)

简介说明：正态化的ATR，注意正态化后的范围



### True Range——真实波动幅度 

代码：TRANGE(high, low, close)      

简介说明：前交易日的最高价与最低价间的波幅，前一交易日收盘价与当个交易日最高价间的波幅，前一交易日收盘价与当个交易日最低价间的波幅，这三者中的最大值为真实波幅

6. Price Transform Functions(价格转换)
价格转换，在TALib中价格转换函数有4个，汇总如下：



### Average Price——平均价格

代码：AVGPRICE(open, high, low, close) 

简介说明：最高价，开盘价，最低价，收盘价的均值



### Median Price——中位数价格         

代码：MEDPRICE(high, low)

简介说明：最高价和最低价的均值



### Typical Price——典型价格             

代码：TYPPRICE(high, low, close)

简介说明：最高价，最低价，收盘价的均值



### Weighted Close Price——加权收盘价           

代码：WCLPRICE(high, low, close)

简介说明：最高价，最低价和收盘价的加权平均

7. Cycle Indicator Functions(周期指标)
周期性指标常常用来判断中长期的趋势，在TALib中周期性指标有5个，汇总如下：



### Hilbert Transform - Dominant Cycle Period——主导周期期限 

代码：HT_DCPERIOD(close)

简介说明：略





### Hilbert Transform - Dominant Cycle Phase——主导周期阶段  

代码：HT_DCPHASE(close)

简介说明：略



### Hilbert Transform - Phasor Components——相位构成      

代码：HT_PHASOR(close)

简介说明：略



### Hilbert Transform – SineWave——正弦波    

代码：HT_SINE(close)

简介说明：略



### Hilbert Transform - Trend vs Cycle Mode——趋势-周期模式   

代码：HT_TRENDMODE(close)

简介说明：略


# Pattern Recognition Functions(模式识别函数)
在TALib中模式识别函数非常多，对应了技术分析中很多量价形态和模式，按模式期限汇总如下。 在这一节中，有些术语先在这里说明，x日K线模式指的是x交易日周期的K线模式，上影线指的是最高价-max(开盘价，收盘价)的长度，下影线指的是最低价-min(开盘价，收盘价)的长度，向上跳空指的是T日最低价大于T-1日最高价，向下跳空指的是T日最高价小于T-1日最低价。

在模式识别函数的输出中，0表示该日无这一模式，100表示在改日识别了这一模式，-100表示在改日识别了这一模式的反向模式。

### 一日K线模式
Closing Marubozu  收盘缺影线

代码：ta.CDLCLOSINGMARUBOZU(open, high, low, close)

简介说明：一日K线模式，以阳线为例，最低价低于开盘价，收盘价等于最高价，预示着趋势持续



### Doji 十字

代码：ta.CDLDOJI(open, high, low, close)

简介说明：一日K线模式，开盘价与收盘价基本相同



### Doji Star 十字星

代码：ta.CDLDOJISTAR(open, high, low, close)

简介说明：一日K线模式，开盘价与收盘价基本相同，上下影线不会很长，预示着当前趋势反转



### Dragonfly Doji 蜻蜓十字/T形十字

代码：ta.CDLDRAGONFLYDOJI(open, high, low, close)

简介说明：一日K线模式，开盘后价格一路走低，之后收复，收盘价与开盘价相同，预示趋势反转



### Gravestone Doji 墓碑十字/倒T十字

代码：ta.CDLGRAVESTONEDOJI(open, high, low, close)

简介说明：一日K线模式，开盘价与收盘价相同，上影线长，无下影线，预示底部反转



### Hammer 锤头

代码：ta.CDLHAMMER(open, high, low, close)

简介说明：一日K线模式，实体较短，无上影线，下影线大于实体长度两倍，处于下跌趋势底部，预示反转



### Hanging Man 上吊线

代码：ta.CDLHANGINGMAN(open, high, low, close)

简介说明：一日K线模式，形状与锤子类似，处于上升趋势的顶部，预示着趋势反转



### Inverted Hammer 倒锤头

代码： ta.CDLINVERTEDHAMMER(open, high, low, close)

简介说明：一日K线模式，上影线较长，长度为实体2倍以上，无下影线，在下跌趋势底部，预示着趋势反转



### Long Legged Doji 长脚十字

代码：ta.CDLLONGLEGGEDDOJI(open, high, low, close)

简介说明：一日K线模式，开盘价与收盘价相同居当日价格中部，上下影线长，表达市场不确定性



### Long Line Candle长蜡烛

代码： ta.CDLLONGLINE(open, high, low, close)

简介说明：一日K线模式，K线实体长，无上下影线



### Marubozu 光头光脚/缺影线

代码：ta.CDLMARUBOZU(open, high, low, close)

简介说明：一日K线模式，上下两头都没有影线的实体，阴线预示着熊市持续或者牛市反转，阳线相反



### Rickshaw Man 黄包车夫

代码：ta.CDLRICKSHAWMAN(open, high, low, close)

简介说明：一日K线模式，与长腿十字线类似，若实体正好处于价格振幅中点，称为黄包车夫



### Separating Lines 分离线

代码：ta.CDLSEPARATINGLINES(open, high, low, close)

简介说明：一日K线模式，上影线至少为实体长度两倍，没有下影线，预示着股价下跌



### Shooting Star 射击之星

代码：ta.CDLSHOOTINGSTAR(open, high, low, close)

简介说明：一日K线模式，上影线至少为实体长度两倍，没有下影线，预示着股价下跌



### Short Line Candle 短蜡烛

代码：ta.CDLSHORTLINE(open, high, low, close)

简介说明：一日K线模式，实体短，无上下影线



### Takuri (Dragonfly Doji with very long lower shadow)探水竿

代码：ta.CDLTAKURI(open, high, low, close)

简介说明：一日K线模式，大致与蜻蜓十字相同，下影线长度长

# 二日K线模式
### Belt-hold 捉腰带线

代码：ta.CDLBELTHOLD(open, high, low, close)

简介说明：二日K线模式，下跌趋势中，第一日阴线，第二日开盘价为最低价，阳线，收盘价接近最高价，预示价格上涨


### Counterattack反击线

代码：ta.CDLCOUNTERATTACK(open, high, low, close)

简介说明：二日K线模式，与分离线类似



### Dark Cloud Cover 乌云压顶

代码：ta.CDLDARKCLOUDCOVER(open, high, low, close, penetration=0)

简介说明：二日K线模式，第一日长阳，第二日开盘价高于前一日最高价，收盘价处于前一日实体中部以下，预示着股价下跌



### Engulfing Pattern 吞噬模式

代码：ta.CDLENGULFING(open, high, low, close)

简介说明：二日K线模式，分多头吞噬和空头吞噬，以多头吞噬为例，第一日为阴线，第二日阳线，第一日的开盘价和收盘价在第二日开盘价收盘价之内，但不能完全相同



### Up/Down-gap side-by-side white lines 向上/下跳空并列阳线

代码：ta.CDLGAPSIDESIDEWHITE(open, high, low, close)

简介说明：二日K线模式，上升趋势向上跳空，下跌趋势向下跳空，第一日与第二日有相同开盘价，实体长度差不多，则趋势持续



### Harami Pattern 母子线

代码： ta.CDLHARAMI(open, high, low, close)

简介说明：二日K线模式，分多头母子与空头母子，两者相反，以多头母子为例，在下跌趋势中，第一日K线长阴，第二日开盘价收盘价在第一日价格振幅之内，为阳线，预示趋势反转，股价上升



### Harami Cross Pattern  十字孕线

代码：ta.CDLHARAMICROSS(open, high, low, close)

简介说明：二日K线模式，与母子县类似，若第二日K线是十字线，便称为十字孕线，预示着趋势反转转



### Homing Pigeon 家鸽

代码：ta.CDLHOMINGPIGEON(open, high, low, close)

简介说明：二日K线模式，与母子线类似，不同的的是二日K线颜色相同，第二日最高价、最低价都在第一日实体之内，预示着趋势反转



### In-Neck Pattern 颈内线

代码：ta.CDLINNECK(open, high, low, close)

简介说明：二日K线模式，下跌趋势中，第一日长阴线，第二日开盘价较低，收盘价略高于第一日收盘价，阳线，实体较短，预示着下跌继续



### Kicking 反冲形态

代码：ta.CDLKICKING(open, high, low, close)

简介说明：二日K线模式，与分离线类似，两日K线为秃线，颜色相反，存在跳空缺口



### Kicking - bull/bear determined by the longer marubozu 由较长缺影线决定的反冲形态

代码：ta.CDLKICKINGBYLENGTH(open, high, low, close)

简介说明：二日K线模式，与反冲形态类似，较长缺影线决定价格的涨跌



### Matching Low 相同低价

代码： ta.CDLMATCHINGLOW(open, high, low, close)

简介说明：二日K线模式，下跌趋势中，第一日长阴线，第二日阴线，收盘价与前一日相同，预示底部确认，该价格为支撑位



### On-Neck Pattern 颈上线

代码： ta.CDLONNECK(open, high, low, close)

简介说明：二日K线模式，下跌趋势中，第一日长阴线，第二日开盘价较低，收盘价与前一日最低价相同，阳线，实体较短，预示着延续下跌趋势



### Piercing Pattern刺透形态

代码：a.CDLPIERCING(open, high, low, close)

简介说明：二日K线模式，下跌趋势中，第一日阴线，第二日收盘价低于前一日最低价，收盘价处在第一日实体上部，预示着底部反转

### Thrusting Pattern 插入

代码：ta.CDLTHRUSTING(open, high, low, close)

简介说明：二日K线模式，与颈上线类似，下跌趋势中，第一日长阴线，第二日开盘价跳空，收盘价略低于前一日实体中部，与颈上线相比实体较长，预示着趋势持


# 三日K线模式
### Two Crows 两只乌鸦

代码：ta.CDL2CROWS(open, high, low, close)

简介说明：三日K线模式，第一天长阳，第二天高开收阴，第三天再次高开继续收阴，收盘比前一日收盘价低，预示股价下跌



### Three Black Crows 三只乌鸦

代码：ta.CDL3BLACKCROWS(open, high, low, close)

简介说明：三日K线模式，连续三根阴线，每日收盘价都下跌且接近最低价，每日开盘价都在上根K线实体内，预示股价下跌



### Three Inside Up/Down 三内部上涨和下跌

代码：ta.CDL3INSIDE(open, high, low, close)

简介说明：三日K线模式，母子信号+长K线，以三内部上涨为例，K线为阴阳阳，第三天收盘价高于第一天开盘价，第二天K线在第一天K线内部，预示着股价上涨



### Three Outside Up/Down 三外部上涨和下跌

代码：ta.CDL3OUTSIDE(open, high, low, close)

简介说明：三日K线模式，与三内部上涨和下跌类似，K线为阴阳阳，但第一日与第二日的K线形态相反，以三外部上涨为例，第一日K线在第二日K线内部，预示着股价上涨



### Three Stars In The South 南方三星

代码：ta.CDL3STARSINSOUTH(open, high, low, close)

简介说明：三日K线模式，与大敌当前相反，三日K线皆阴，第一日有长下影线，第二日与第一日类似，K线整体小于第一日，第三日无下影线实体信号，成交价格都在第一日振幅之内，预示下跌趋势反转，股价上升



### Three Advancing White Soldiers 三个白兵

代码：ta.CDL3WHITESOLDIERS(open, high, low, close)

简介说明：三日K线模式，三日K线皆阳，每日收盘价变高且接近最高价，开盘价在前一日实体上半部，预示股价上升



### Abandoned Baby 弃婴

代码： ta.CDLABANDONEDBABY(open, high, low, close, penetration=0)

简介说明：三日K线模式，第二日价格跳空且收十字星（开盘价与收盘价接近，最高价最低价相差不大），预示趋势反转，发生在顶部下跌，底部上涨



### Advance Block 大敌当前

代码：ta.CDLADVANCEBLOCK(open, high, low, close)

简介说明：三日K线模式，三日都收阳，每日收盘价都比前一日高，开盘价都在前一日实体以内，实体变短，上影线变长



### Evening Doji Star 十字暮星

代码：ta.CDLEVENINGDOJISTAR(open, high, low, close, penetration=0)

简介说明：三日K线模式，基本模式为暮星，第二日收盘价和开盘价相同，预示顶部反转



### High-Wave Candle 风高浪大线

代码：ta.CDLHIGHWAVE(open, high, low, close)

简介说明：三日K线模式，具有极长的上/下影线与短的实体，预示着趋势反转转



### Hikkake Pattern 陷阱

代码： ta.CDLHIKKAKE(open, high, low, close)

简介说明：三日K线模式，与母子类似，第二日价格在前一日实体范围内，第三日收盘价高于前两日，反转失败，趋势继续



### Modified Hikkake Pattern 修正陷阱

代码：ta.CDLHIKKAKEMOD(open, high, low, close)

简介说明：三日K线模式，与陷阱类似，上升趋势中，第三日跳空高开；下跌趋势中，第三日跳空低开，反转失败，趋势继续



### Identical Three Crows 三胞胎乌鸦

代码：ta.CDLIDENTICAL3CROWS(open, high, low, close)

简介说明：三日K线模式，上涨趋势中，三日都为阴线，长度大致相等，每日开盘价等于前一日收盘价，收盘价接近当日最低价，预示价格下跌



### Morning Doji Star 十字晨星

代码：ta.CDLMORNINGDOJISTAR(open, high, low, close, penetration=0)

简介说明：三日K线模式，基本模式为晨星，第二日K线为十字星，预示底部反转



### Morning Star 晨星

代码：ta.CDLMORNINGSTAR(open, high, low, close, penetration=0)

简介说明：三日K线模式，下跌趋势，第一日阴线，第二日价格振幅较小，第三天阳线，预示底部反转



### Stalled Pattern 停顿形态

代码：ta.CDLSTALLEDPATTERN(open, high, low, close)

简介说明：三日K线模式，上涨趋势中，第二日长阳线，第三日开盘于前一日收盘价附近，短阳线，预示着上涨结束



### Stick Sandwich 条形三明治

代码：ta.CDLSTICKSANDWICH(open, high, low, close)

简介说明：三日K线模式，第一日长阴线，第二日阳线，开盘价高于前一日收盘价，第三日开盘价高于前两日最高价，收盘价于第一日收盘价相同



### Tasuki Gap 跳空并列阴阳线

代码：ta.CDLTASUKIGAP(open, high, low, close)

简介说明：三日K线模式，分上涨和下跌，以上升为例，前两日阳线，第二日跳空，第三日阴线，收盘价于缺口中，上升趋势持续



### Tristar Pattern 三星

代码：ta.CDLTRISTAR(open, high, low, close)

简介说明：三日K线模式，由三个十字组成，第二日十字必须高于或者低于第一日和第三日，预示着反转



### Unique 3 River 奇特三河床

代码： ta.CDLUNIQUE3RIVER(open, high, low, close)

简介说明：三日K线模式，下跌趋势中，第一日长阴线，第二日为锤头，最低价创新低，第三日开盘价低于第二日收盘价，收阳线，收盘价不高于第二日收盘价，预示着反转，第二日下影线越长可能性越大



### Upside Gap Two Crows 向上跳空的两只乌鸦

代码：ta.CDLUPSIDEGAP2CROWS(open, high, low, close)

简介说明：三日K线模式，第一日阳线，第二日跳空以高于第一日最高价开盘，收阴线，第三日开盘价高于第二日，收阴线，与第一日比仍有缺口

# 四日K线模式
### Three-Line Strike三线打击

代码：CDL3LINESTRIKE(open, high, low, close)

简介说明：四日K线模式，前三根阳线，每日收盘价都比前一日高，开盘价在前一日实体内，第四日市场高开，收盘价低于第一日开盘价，预示股价下跌



### Concealing Baby Swallow藏婴吞没

代码：CDLCONCEALBABYSWALL(open, high, low, close)

简介说明：四日K线模式，下跌趋势中，前两日阴线无影线，第二日开盘、收盘价皆低于第二日，第三日倒锤头，第四日开盘价高于前一日最高价，收盘价低于前一日最低价，预示着底部反转

# 五日K线模式

### Breakaway脱离

代码：CDLBREAKAWAY(open, high, low, close)

简介说明：五日K线模式，以看涨脱离为例，下跌趋势中，第一日长阴线，第二日跳空阴线，延续趋势开始震荡，第五日长阳线，收盘价在第一天收盘价与第二天开盘价之间，预示价格上涨



### Ladder Bottom梯底

代码：CDLLADDERBOTTOM(open, high, low, close)

简介说明：五日K线模式，下跌趋势中，前三日阴线，开盘价与收盘价皆低于前一日开盘、收盘价，第四日倒锤头，第五日开盘价高于前一日开盘价，阳线，收盘价高于前几日价格振幅，预示着底部反转

### Mat Hold铺垫

代码：CDLMATHOLD(open, high, low, close, penetration=0)

简介说明：五日K线模式，上涨趋势中，第一日阳线，第二日跳空高开影线，第三、四日短实体影线，第五日阳线，收盘价高于前四日，预示趋势持续



### Rising/Falling Three Methods上升/下降三法

代码：CDLRISEFALL3METHODS(open, high, low, close)

简介说明：五日K线模式，以上升三法为例，上涨趋势中，第一日长阳线，中间三日价格在第一日范围内小幅震荡，第五日长阳线，收盘价高于第一日收盘价，预示股价上升



### Upside/Downside Gap Three Methods上升/下降跳空三法

代码：CDLXSIDEGAP3METHODS(open, high, low, close)

简介说明：五日K线模式，以上升跳空三法为例，上涨趋势中，第一日长阳线，第二日短阳线，第三日跳空阳线，第四日阴线，开盘价与收盘价于前两日实体内，第五日长阳线，收盘价高于第一日收盘价，预示股价上升

# Statistic Functions(统计函数)
在TALib中也提供了很多基础统计函数，汇总如下：



### Beta

代码：BETA(high, low, timeperiod=5)

简介说明：高价序列和低价序列之间的beta值，可通过回归得到



### Pearson's Correlation Coefficient (r) Pearson相关系数

代码：CORREL(high, low, timeperiod=30)

简介说明：高价序列和低价序列的线性相关系数


### Linear Regression 线性回归

代码：LINEARREG(close, timeperiod=14)

简介说明：收盘价序列对时间t的线性回归，并输出预测值

### Linear Regression Angle      线性回归角度     

代码：LINEARREG_ANGLE(close, timeperiod=14)

简介说明：收盘价序列对时间t的线性回归斜率的正切角度



### Linear Regression Intercept       线性回归截距项

代码：LINEARREG_INTERCEPT(close, timeperiod=14)

简介说明：收盘价序列对时间t的线性回归的截距项



### Linear Regression Slope      线性回归斜率

代码：LINEARREG_SLOPE(close, timeperiod=14)

简介说明：收盘价序列对时间t的线性回归的斜率



### Standard Deviation     标准差

代码：STDDEV(close, timeperiod=5, nbdev=1)

简介说明：每5个收盘价计算标准差



### Time Series Forecast时间序列预测

代码：TSF(close, timeperiod=14)      

简介说明：收盘价的时间序列分析预测值



### Variance 方差

代码：VAR(close, timeperiod=5, nbdev=1)

简介说明：每5个收盘价计算方差

15. Math Transform Functions(数学转换函数)
在TALib中也提供了很多数学转换函数，这些函数可以对一个向量来操作，突破了很多函数只能对单个值操作的限制，汇总如下：



### Vector Trigonometric ACos

代码：ACOS(close)

简介说明：反余弦



### Vector Trigonometric ASin

代码：ASIN(close)

简介说明：反正弦



### Vector Trigonometric ATan

代码：ATAN(close)

简介说明：反正切



### Vector Ceil

代码：CEIL(close)

简介说明：向上取整



### Vector Trigonometric Cos

代码：COS(close)

简介说明：余弦



### Vector Trigonometric Cosh

代码：COSH(close)

简介说明：双曲余弦



### Vector Arithmetic Exp

代码：EXP(close)

简介说明：指数



### Vector Floor

代码：FLOOR(close)

简介说明：向下取整



### Vector Log Natural     

代码：LN(close)

简介说明：自然对数



### Vector Log10

代码：LOG10(close)

简介说明：10为底对数



### Vector Trigonometric Sin

代码：SIN(close)

简介说明：正弦



### Vector Trigonometric Sinh 

代码：SINH(close)

简介说明：双曲正弦



### Vector Square Root

代码：SQRT(close)

简介说明：平方根



### Vector Trigonometric Tan

代码：TAN(close)

简介说明：正切



### Vector Trigonometric Tanh

代码：TANH(close)

简介说明：双曲正切

16. Math Operator Functions(数学运算函数)
在TALib中也提供了很多数学运算函数，汇总如下：



### Vector Arithmetic Add       

代码：ADD(high, low)

简介说明：相加(高价+低价)



### Vector Arithmetic Div        

代码：DIV(high, low)

简介说明：相除(高价/低价)



### Highest value over a specified period       

代码：MAX(close, timeperiod=30)

简介说明：指定期间的最大值



### Index of highest value over a specified period

代码：MAXINDEX(close, timeperiod=30)

简介说明：指定期间最大值的索引



### Lowest value over a specified period        

代码：MIN(close, timeperiod=30)

简介说明：指定期间的最小值



### Index of lowest value over a specified period

代码：MININDEX(close, timeperiod=30)

简介说明：指定期间最小值的索引



### Lowest and highest values over a specified period  

代码：MINMAX(close, timeperiod=30)

简介说明：指定期间的最大值和最小值



### Indexes of lowest&highest values over a period

代码：MINMAXINDEX(close, timeperiod=30)

简介说明：指定期间最大值和最小值的索引



### Vector Arithmetic Mult      

代码：MULT(high, low)

简介说明：相乘(高价*低价)     



### Vector Arithmetic Substraction

代码：SUB(high, low)

简介说明：相减(高价-低价)



### Summation

代码：SUM(close, timeperiod=30)

简介说明：指定期间的加总
