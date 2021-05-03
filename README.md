# vut-ios-project1
Bash Shell script logs parcer

The COMMAND can be one of: \
list-tick - a list of occurring stock exchange "ticks"\
profit - statement of total profit from closed positions\
pos - list of values of currently held positions sorted in descending order by value\
last-price - a listing of the last known price for each ticker\
hist-ord - list of histogram of the number of transactions according to the ticker\
graph-pos - list of graph of values of held positions according to the ticker

The FILTER can be a combination of the following: \
-a DATETIME - after: only records after this date are considered (without this date). DATETIME is in the format YYYY-MM-DD HH: MM: SS\
-b DATETIME - before: only records BEFORE this date (without this date) are considered\
-t TICKER - only records corresponding to the given ticker are considered. With multiple occurrences of the switch, the set of all listed ticker is taken\
-w WIDTH - sets the width of the graph listing, ie the length of the longest line to WIDTH. Thus, WIDTH must be a positive integer. Multiple occurrences of the switch is a faulty start\
-h and --help print help with a brief description of each command and switch\

.logs format: DATE AND TIME; TICKER; TRANSACTION TYPE; UNIT PRICE; CURRENCY; VOLUME; ID\
Example: \
2021-07-29 23:43:13;TSLA;buy;667.90;USD;306;65fb53f6-7943-11eb-80cb-8c85906a186d \

Examples: \
$ cat stock-2.log | head -n 5 | ./tradelog
2021-07-29 15:30:42;MSFT;sell;240.07;USD;327;65fad854-7943-11eb-929d-8c85906a186d
2021-07-29 15:31:12;MA;sell;314.91;USD;712;65fae24a-7943-11eb-9171-8c85906a186d
2021-07-29 15:31:32;BAC;buy;34.16;USD;635;65fae466-7943-11eb-8f48-8c85906a186d
2021-07-29 15:37:09;BAC;sell;36.67;USD;897;65fae614-7943-11eb-9ccb-8c85906a186d
2021-07-29 15:43:02;JPM;sell;146.77;USD;190;65fae79a-7943-11eb-8977-8c85906a186d

$ ./tradelog -t TSLA -t V stock-2.log
2021-07-29 17:06:57;TSLA;buy;757.57;USD;812;65fafb04-7943-11eb-8d41-8c85906a186d
2021-07-29 17:58:18;V;sell;215.31;USD;406;65fb0662-7943-11eb-87fe-8c85906a186d
2021-07-29 18:12:27;TSLA;sell;729.75;USD;482;65fb0892-7943-11eb-867f-8c85906a186d
2021-07-29 18:55:19;V;sell;217.92;USD;210;65fb1238-7943-11eb-86e2-8c85906a186d
2021-07-29 19:19:26;TSLA;sell;700.75;USD;457;65fb1792-7943-11eb-8abf-8c85906a186d
2021-07-29 19:27:39;TSLA;buy;710.79;USD;633;65fb19b8-7943-11eb-a5d9-8c85906a186d
2021-07-29 20:06:53;V;sell;218.72;USD;272;65fb237c-7943-11eb-83a3-8c85906a186d
2021-07-29 20:59:16;V;sell;196.54;USD;92;65fb2c32-7943-11eb-9dd3-8c85906a186d
2021-07-29 21:03:15;V;buy;188.60;USD;605;65fb2d4a-7943-11eb-8804-8c85906a186d
2021-07-29 21:17:37;V;sell;222.52;USD;447;65fb2f7a-7943-11eb-8f28-8c85906a186d
2021-07-29 21:18:18;TSLA;buy;733.96;USD;720;65fb3092-7943-11eb-992a-8c85906a186d
2021-07-29 21:50:25;V;sell;212.58;USD;2833;65fb3a2e-7943-11eb-8e0b-8c85906a186d
2021-07-29 22:10:55;TSLA;sell;718.31;USD;3794;65fb3f88-7943-11eb-a371-8c85906a186d
2021-07-29 22:21:31;TSLA;sell;681.74;USD;7122;65fb41a4-7943-11eb-a09f-8c85906a186d
2021-07-29 23:01:47;TSLA;sell;707.03;USD;1578;65fb4a50-7943-11eb-9f6e-8c85906a186d
2021-07-29 23:21:11;TSLA;buy;679.27;USD;9655;65fb4fb4-7943-11eb-8199-8c85906a186d
2021-07-29 23:43:13;TSLA;buy;667.90;USD;306;65fb53f6-7943-11eb-80cb-8c85906a186d
2021-07-29 23:48:29;V;buy;195.52;USD;2003;65fb5824-7943-11eb-9b59-8c85906a186d

$ ./tradelog -t CVX stock-4.log.gz | head -n 3
2021-09-27 05:12:30;CVX;sell;108.17;USD;88;8f229a62-7945-11eb-a6fb-8c85906a186d
2021-09-27 13:57:48;CVX;sell;94.81;USD;5374;8f22ec38-7945-11eb-8c68-8c85906a186d
2021-09-27 14:52:50;CVX;sell;89.22;USD;7759;8f22f46c-7945-11eb-9bb2-8c85906a186d

$ ./tradelog list-tick stock-2.log
AAPL
AMZN
BABA
BAC
DIS
FB
GOOG
GOOGL
JNJ
JPM
MA
MSFT
NVDA
PG
PYPL
TSLA
TSM
UNH
V
WMT

$ ./tradelog profit stock-2.log
-58863165.03

$ ./tradelog -t TSM -t PYPL profit stock-2.log
-577302.62

$ ./tradelog pos stock-2.log
AMZN      : 64645275.64
GOOGL     :  7914389.08
NVDA      :  2540507.69
DIS       :  1925621.88
TSM       :  1266217.38
JPM       :   937220.31
BABA      :   444692.64
BAC       :   323899.29
JNJ       :    81769.32
FB        :    42673.05
WMT       :     2423.34
MSFT      :  -321051.64
V         :  -322999.04
PYPL      :  -502892.46
MA        :  -569746.42
TSLA      :  -872945.30
PG        : -1138885.10
AAPL      : -1190996.48
UNH       : -1781240.88
GOOG      : -9846258.51

$ ./tradelog -t TSM -t PYPL -t AAPL pos stock-2.log
TSM       :  1266217.38
PYPL      :  -502892.46
AAPL      : -1190996.48

$ ./tradelog last-price stock-2.log
AAPL      :  133.88
AMZN      : 3496.04
BABA      :  245.28
BAC       :   38.61
DIS       :  207.48
FB        :  275.31
GOOG      : 1975.97
GOOGL     : 1990.04
JNJ       :  155.16
JPM       :  135.77
MA        :  333.38
MSFT      :  237.64
NVDA      :  629.93
PG        :  124.70
PYPL      :  279.54
TSLA      :  667.90
TSM       :  140.41
UNH       :  321.06
V         :  195.52
WMT       :  134.63

$ ./tradelog hist-ord stock-2.log
AAPL      : ##
AMZN      : #####
BABA      : ####
BAC       : #####
DIS       : #####
FB        : ####
GOOG      : ######
GOOGL     : ########
JNJ       : ##
JPM       : ######
MA        : ####
MSFT      : ####
NVDA      : ######
PG        : #####
PYPL      : ####
TSLA      : ##########
TSM       : ##
UNH       : ######
V         : ########
WMT       : ####

$ ./tradelog -w 100 graph-pos stock-6.log
AAPL      : !!!!!!!!!!!!
AMZN      : !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
BABA      : ####
BAC       : ###
DIS       : ###################
FB        :
GOOG      : !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
GOOGL     : ################################################################################
JNJ       :
JPM       : #########
MA        : !!!!!
MSFT      : !!!
NVDA      : #########################
PG        : !!!!!!!!!!!
PYPL      : !!!!!
TSLA      : !!!!!!!!
TSM       : ############
UNH       : !!!!!!!!!!!!!!!!!!
V         : !!!
WMT       :

$ ./tradelog -w 10 -t FB -t JNJ -t WMT graph-pos stock-6.log
FB        : #####
JNJ       : ##########
WMT       :

$ cat /dev/null | ./tradelog profit
0.00

