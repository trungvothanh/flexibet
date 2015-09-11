
```

Start: 12.10 - 23.10
- 3 - WebConsole: Display slope on a hist prices chart.
- 2 - Console: Display total liability
- 1 - Console: Display num of bets that the liability was calculated for.
- 2 - Console: Display liability/num of bets for markets that aren't in play.
- 3 - Add all required fields to account_statement table in db - to break dependency to runner_state_bet and to improve performance.
Total: 11

Start: 28.09 - 09.10
- 5 - Create betex-archive-sql (store market, runners and runnerprices).
- 5 - Create replay prototype.
- 5 - Create a betting simulator
- 5 - Add separate task to monitor HR markets 10 mins before markets time. Check if it is thread safe regarding to other tasks.
- 2 - Add market filter to bot config to monitor in play markets.
- 2 - BettingConsole: Connect history chart in statement module to betex-archive-sql data. 
- 3 - Creating betexInFrontOFQueue impl
- 1 - Keep only a max number of data per market in a regression cache.
- 2 - Remove data older than 3h from a regression cache during a night.
- 1 - Improve performance of betting simulator.
Total: 31

Start: 14.09 - 25.09
- 1 - Move AccountStatementTask/RemoveOldStateMachines from bettingEngine to flexiBet-server.
- 1 - Move RunnnerStateDao.findRunnerState(betId) to bettingServer.
- 1 - Move BetsDao from bettingEngine to bettingServer.
- 1 - Move RunnerStateDAO.getRunnerStateBets from bettingEngine to bettingServer
- 2 - Replace betFairService with a betApi in a bettingEngine.
- 2 - Return list of placed bets by a bettingEngine.fireEvent method.
- 3 - Move RunnerStateDAO.addRunnerStateBet from bettingEngine to bettingServer
- 1 - StateMachineResult - add runnerStateId, so then marketRunnerListener doesn't need to get runner state from db before adding bet to db.
- 3 - RunnerStateLastBetDAO().addBet - move it from bettingEngine to bettingServer.
- 1 - Create a bettingEngineDao.findRunnerState and use it in a RunnerStateCache.
- 1 - Return inputStateName/outputStateName in a bettingEngine results, so modified states can be saved in a db.
- 1 - Save modified runner states in a marketRunnerListener ( betting-server) and remove saveRunnerState from a runnerStateCache.
- 2 - Remove dependency to a lastBetDao in a bettingEngine.
- 1 - Remove dependency to a datasource in a bettingEngine.
- 3 - Implement stop bot.
- 3 - Refactor MarketObserver: marketModel.
- 2 - MarketObserver: Remove marketDetails and move marketDetailsRunners to marketData.
Total: 29

Start: 31.08 - 11.09
- 2 - Analyze performance of RunnerServiceImpl
- 2 - BetextArchive: Create design of market history module.
- 3 - BetextArchive: Create archetype of GAE application and deploy it to GAE.
- 2 - BetextArchive: Create domain model and parser for LastMatchedPrice object.
- 3 - BetextArchive: Implement storePrice and create integrationTest.
- 3 - BetextArchive: Implement getPrices and create integrationTest.
- 2 - BettingApp: Publish last matched runner prices on a betex history application (Google Apps Engine).
- 3 - BetexArchive: Create getPricesChartRequest to display chart with last matched prices for market runner.
- 3 - WebConsole: Display chart in account statement module with last matched price for market runner.
- 2 - Create a betting app maven module.
- 2 - Virt bets are always empty in betting engine - remove virtual bets concept.
- 5 - Refactor MarketRunnerListener, move it to the betting app and call from it a betting engine and betexArchivePublisher.
- 3 - Move StateMachineConfigLoader to the betting app.
- 2 - BetexArchive: Refactor BetexArchive to use Guice framework
- 1 - BetexArchive: Refactor getPrices/getPricesChart to use common business logic.
- 1 - BetexArchive: Refactor storePrices to use DAO object.
- 1 - Add chart with last runner matched probability to betex archive.
- 2 - Add slope to betex archive.
- 2 - Modify flexibet to send slope to betex archive.
- 1 - Order account statement by settledDate and placedDate.
- 1 - Add lastBet.matchedDate to runner context.
Total 46


Start: 17.08 - 29.08
- 1 - Add checkTxLimit parameter to BetFairService.placeBet()
- 2 - add market.isTurningInPlay to runner context.
- 2 - Add checkTxCounter to placeBet action.  
- 1 - Console account statement module: add periods: last 30 days, last 3 months. 
- 1 - Console account statement module: display first 100 items.
- 2 - Check how NaN works in scxml expressions.
Total 9

Start: 27.07 - 07.08
- 5 - BetDaq->BF placeBet
- 3 - BetDaq->BF cancelBet
- 3 - BetDaq->BF getAccountFunds
- 3 - BetDaq->BF getAccountStatement
Total 14

Start: 13.07 - 24.07
- 5 - Add non bet account statement items to db and display then in account statement module.
- 3 - Add marketDetails panel link from betsStat.
- 3 - Add list of bets from betsStat (betId, placedDate, price)
- 3 - BetDaq->BF getMarkets
- 3 - BetDaq->BF getMarketDetails
- 3 - BetDaq->BF getBets
- 5 - BetDaq->BF getMarketRunners
- 3 - BetDaq->BF getBetFairServiceInfo
- 3 - BetDaq->ladderPrices
Total 31

Start: 29.06 - 10.07
- 5 - Refactor scheduled tasks. Create services layer and design the beanstat better. Currently the same code is in each task. Also check if only tasks have bean statistics, e.g. BwinService.
- 1 - Remove BeanStat from Bwin module.
- 2 - Add filter by state name to account statement.
- 1 - Add show this week to account statement.
- 1 - BetFairService - throw exception by placeBet when tx limit is reached.
- 8 - Refactor MarketService to use BFMarkets, Massey and Racing post, BWin caches.
- 4 - Refactor SystemModule - expose market observer through JMX and create jmx client in system module.
- 3 - Console stats: how many bets are placed in each hour of the day.
- 3 - Expose BettingEngine through jmx. 
Total 28

Start: 15.05 - 26.05
- 3 - Create MarketDetails page.
- 1 - Display total commission in a account statement module. 
- 1 - Add date/time to console header
- 3 - Add statemachine filter to account statement in console
- 1 - Console statement module - order by settled date/stake
- 1 - Add bets amount to account statement in console
- 3 - Break dep between StateMachineServiceConfigFactoryBean and BotConfig (create groovy file for state machines.
- 1 - State machine order.
- 1 - Bot can't be started if betfair server is down - simplest solution.
- 3 - Remove BotConfig and replace it with context:property-placeholder.
- 1 - Add jdbc config to the bot.properties.
- 2 - Create BetFairServiceFactoryBean to return real/test BetFairService.
- 1 - Remove BotHelper.getProductionMode
- 2 - Refactor Betting engine to use one RunnerContextFactory - currently there are two.
- 1 - Two state machines: 1 has no market filers, second has soccer filter, then first machine will analyze only soccer. If no market filters then state machine should analyze nothing. 
- 3 - Remove hack for monitoring HR and bwin matched sports in RunnerServiceImpl.
- 8 - Compare HR odds with http://www.adrianmassey.com/index.php
- 5 - Adapter to racing post.
- 5 - Add racing post price to runner context and to market details screen.
Total 46

Start: 04.05 - 15.05
- 5 - Support multiple state machines in console statesStat panel.
- 5 - Support multiples state machines in facade.
- 3 - Support multiple state machines - load multiple state machine from directory.
- 5 - Support multiple state machines in StatesMachinesService.
- 8 - Support multiple state machines in RunnerService.
- 2 - Support multiple state machines in database.
Total 28

Start: 18.05 - 29.05
- 13 - Create flexibet-marketobserver
- 5 - Create betting-engine module
- 5 - Create MarketObserver bean
- 3 - Refactor market observer to use market filters from state machines info files.
- 3 - Bwin adapter doesn't work.
- 2 - Add Market details window to account statement module.
- 1 - Add to bets the marketId.
- 2 - Add Market details window to bets module.
Total 34

Start: 01.05 - 12.05
- 5 - Modify StateMachineService to create state machines only for required runners, e.g. hr state machine don't need to analyze football markets., To test it create new state machine with market filter for soccer and state for hr.
- 2 - Add weighted prices to market details and check why less bets are placed than when weight price was not checked.
- 2 - Add slope/slopeErr to market details.
- 2 - Add deeplink to console: bets module and market details module.
- 1 - Add numOfWinners, numOfRunners to market details console module.
- 3 - Check if priceToBackWeighted and runner.slope/slopeErr are correct.
- 5 - Support multiples state machines in states visits module.
- 1 Add num of bets in current hour to System module in web console.
- 3 - Improve backup (EMC)
- 5 - Organize domain model for BetFairService - create BetFairService with own domain model.
- 3 - Create BettingEngine bean.
Total 32




Release 1.30 (03/05/09)
- Put SP mark to account statement that bet is SP.
- Implement betting exchange placeSPBet.
- Implement placeVirtSPBet action.
- Put to console markets module the timestamp for MarketRunners and marketTime.
- Implement commission on a virtual exchange.
- Analyze markets in play.
- In bets module for matched bets the price is displayed instead of avgMatched.
- In SP Bets req odds change to empty if MoC.
- SPBet do not show liability as stake for SP Lay bets.
- Create system tab on web console (add beans stat, caches, memory, etc.).
- Display SP bets in bets console module.
- Display SP bets in virt bets console module.
- Move matched SP bets to matched bets, currently they are in SP Bets (Odss. req is set for MoC SP bet). Put also a mark that it is a SP bet. 
- Implement bettingExchange reconcileMarketRunner.
- Implement ReconcileMarketsTask.
- Check min. liability for SP lay/back bets.
- Add market.isBspMarket to runner context.
- Put last exceptions to system module in webconsole. 
- Creating two console views: BetFairConsole and VirtualConsole.
- Create WinnerRandomizer/VirtWinnerRandomizer web module.
- Implement placeSPBet action.

Release 1.29 (06/04/09)
- Add 'States visits' tab to the web console.
- Implementing placeSPBet.
- Implement completeMarketsCache.
- Put web console stat for complateMarketsCache (amount of markets).
- Near/Far SP prices are cleared in completeMarketsCache, when market becomes in play - do not clear it.
- Add web module for completeMarkets cache. Display market details and runners for marketId.
- Add settleMarketTask to web console stats.
- Implement marketWinner random generator based on runner winning probability.
- Implement settleMarketTask - settle all markets every 5 mins using randomWinnerGenerator.
- Add console stats for BettingExchange (mBets/uBets amount, , settledMarkets amount)
- Put min bet size=2 and round it to 2 decimal places in placeVirtBet/placeBet actions.
- Implement account statement console module (real and virtual). For today and from yesterday.
- Implement bettingExchange settleMarket() and getAccountStatement().
- Add Virtal Dashboard tab to web console (profit per states for this/last week, the same as for real dashboard).
- Store last best prices before market is turn in play and display in console markets module.
- Implement bets and virtBets console modules.
- UpdateAccountStatementTask should not be run from eclipse.
- Add app start time to web console system stats.
- Implement betting exchange: getBets,placeVirtBet, cancelVirtBet, lastVirtBetBack,lastVirtBetBack, runner.isVirtGreen.
- Change BetFairService.getMarketRunners to return null if market is suspended/closed.

Release 1.28
- Add birt statistics (at least 2) - TESTED
- Near/far/actual sp added to the last_bet_runner. - TESTED
- Last bet matched shows placedDate instead of showing matchedDate. - TESTED
- New Birt report is created: HR_GB_MarketType_Period. -TESTED
- Add market name to the runner context. - TESTED
- State_Period report is added to web_console. - TESTED
- Create runner cache with the recent history - TESTED
- Integrate runner cache with webconsole and add cache size to dashboard. - TESTED
- Implement price linear regression. - TESTED
- Add the linear regression to runner context (trend estimation: up/down). - TESTED
- Replace BetFairUtils.round with MathUtil.round - TESTED
- Create DataRequestsCounter - protection against DataCharge commission. - TESTED
- Create TransactionCounter - protection against TransactionCharge commission. - TESTED
- Create design document. - TESTED
- Add isInPlay to runner context. - TESTED
- Remove old runner states from memory. - TESTED
- Refactor MarketSummary.getAnalyzedMarketsAmount and getAnalyzedRunnersAmount. - TESTED
- Add to web console amount of analyzed in play markets - TESTED.
- Add isInPLay/slope/slopeErr to last_bet_runner. - TESTED
- Modify birt stat for HR_GB_States to choose sport - use birt parameter. - TESTED
- Modify web console stat HR_GB_States to support parameters. - TESTED

```