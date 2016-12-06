# Nelson-Winter-Model

 Nelson and Winter have developed the most influential simulation models to analyze the processes of industrial dynamics and economic growth. Their models are perfect examples of the KISS principle in simulation. The models and the evolutionary theory on which the models are based are explained in detail in their path-breaking book, Nelson, R.R., and Winter, S.G. (1982), _An Evolutionary Theory of Economic Change_, Belknap Press, Cambridge, Mass. and London.

This site provides a simple implementation of the basic industry dynamics model in __R__ so that anybody without a programming knowledge can "play" with the model, run different experiments, and get the feeling of micro-simulation modeling. 

There are two models provided here.

__NELSON WINTER BASE MODEL__

Nelson Winter Base Model is based on the model presented in Nelson and Winter's book (_An Evolutionary Theory of Economic Change_) in Chapter 12. Firms spend a constant amount of money on innovative and imitative R&D activities. More productive firms (thanks to innovation and imitation) become more profitable, make more investment, grow faster, and, consequently, increase their market shares. However, because of the fact that innovation and imitation are random processes in which the probability of innovation and imitation depends on R&D expenditures, there could be shake-ups in market shares. There is no entry and exit in the base model. 

The Nelson-Winter Base Model (R Version) is composed of various functions. In order to run the program, first open the R program, then read the script file (NW_BaseModel.R) by the "source" function. When the script file is read, all functions will be ready. Alternatively, if you use an IDE (like RStudio), open the script file, and run all lines.

The following functions are available in the NW_BaseModel.R script.

__run()__ is the main function that runs the model. It may have three arguments: nIter (number of iterations), nFirm (number of firms) and setSeed (setting the initial seed). The default values are nIter=100, nFirm=8, setSeed=FALSE. In other words, if you simply type,

`run()`

the model will be run for 100 periods for 8 firms, and the initial seed for pseduo-random number generator will use the value it has when the function is run. If you would like to run the model longer (let us say, 500 periods) with more firms, you may type

`run(500, 10, TRUE)`

If you set setSeed value to "TRUE", then the initial seed value for the pseude-random number generator will be equal to 123 (you can change that value to any other one by modifying the "setPara" function). Setting the seed number will guarantee that you can replicate the same simulation anytime you like.

The __run()__ function calls all other functions required to run the program. iterate() is the function that runs the model for one period.

The __setPara()__ function sets parameter values. You can change all parameter values by modifying this function.

The __setFirms()__ and __setMarket()__ functions initialize firms and markets, respectively.

The __invest()__ function calculates the investment level for each firm. __innDraw()__ and __immDraw()__ are innovation and imitation draw functions, respectively.

__pMarket()__ plots four charts about the market outcomes: product price, concentration level, maximum technology (technological frontier) and average technology level. When you run the model, __pMarket()__ function is called by the __run()__ function at the end of simulation, and all these charts are plotted in one page. If you would like to get charts on firm-specific variables, you may use __pMS()__ function that plots markets shares of all firms, and __pTech()__ function that plots technological levels of all firms. __pAccum()__ function plots four charts that help to understand the dynamics of capital accumulation: growth rate of aggregate output, growth rate of aggregate capital stock, average profit rate, and average investment intensity (aggregate investment/capital stock ratio).

To summarize, you can simply type

`run(xx, yy, TRUE)`

to simulate the model for xx periods for yy number of firms. In order to test the effects of random factors, run the same simulation by changing the initial seed as follows:

`run(xx, yy, FALSE)`

__NELSON WINTER ENTRY MODEL__

The Nelson Winter Entry Model is same as the Base Model, but now we allow for entry and exit of firms. The number of entrants increases by the profitability of the market, and those firms that cannot achieve "satisficing" level of profits will exit. Because of the (endogenous) changes in the number of firms, spreadsheets are not suitable tools for these model. Thus, we use R to model the Nelson Wintor Entry Model.

The Nelson Winter Entry Model includes all functions available in the base model. It has two additional functions: __enterFirms()__ and __exitFirms()__. As their names imply, the first function cretaes new firms, and the second function deletes unsuccessful firms. The number of new firms depends on some exogenous parameters and the average profitability in the market. Exit depends on the number of periods with negative profit rate. The user can change parameter values so as to make entry faster and/or strongly correlated with market profitability, and to make exit faster.


