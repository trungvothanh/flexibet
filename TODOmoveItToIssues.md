
```
MUST:
- Console: account statement navigation panel does't reinit dateTime field. 
- BettingEngine: runner.slope is changed to prediction - fix it.
- Console: runner price chart shows inPlay data only for SOCCER markets. Make a form to choose whether or not to show inplay.
- 2 - Replace System.currentTimeMillis with DateTimeUtils.currentTimeMillis() - e.g. to make betting simulator working for hr markets.
- On the recovery don't increase a stake from very low to min if it causes a huge risk, e.g. price 85 and stake 0.5 increased to 2.0
- Add sport_id to betfair api or to market observer as this is used many times using getEventPath.startWith, also it is parsed when writing to market table.
- In MarketRunnerListenerImpl there is a Set of marketIds growing forever. Replace it with an expiring cache, e.g. ehcache, and do the same with other caches, e.g. state machine cache.
- 3 - Extend RemoveStateMachinesTask to remove old data from database: runner_states, market_details
- 2 - Create design of account history module. 
- 3 - Check strategy: compare near/far SP to priceToBack/priceToLay and place exchange bet and SP bet (do it about 10 mins before market turns in play)
- Run more strategies at betdaq.
- Check strategy, place back, lay until runner is green, use stopLoss, slope, racingpost.
- HR - before placing back bet check what was the last amount matched
- HR - Place lay then back gives a huge loss when priceToBack is big, and gives profit when priceToBack<10. So maybe try a strategy to place back then lay for runners when priceToBack is big, e.g. >10 or >15?

- 3 - Place bet action - place bet as the last operation after adding it to the db.
- 2 - Add betType to console BetStats in system module.
- 1 - Set odds for Evs. in racingpost adapter.

- 2 - AdrianMassey adapter is broken and disabled in pom file and in marketservice.
- 3 - Console states visits - add dropdown list with state machine ids.
- 3 - Get market details more than once (market time can change).
- Some betAPI beans are configured inside MarketObserver and some outside - refactor it.
- For betting strategies do not place second bet immediately, wait until it stop growing, also use stop loss.

SHOULD:
- Add warning logging in market_details.market_time!=market.event_date 
- Improve performance of storing bets database by marketRunnerListener - do it in a transaction once a few of them are collected.
- sportId is in a market table but doesn't exist in a MarketData model - inconsistency
- ReconcileVirtMarketsTaskImpl and SettleVirtMarketsTaskImpl are moved to BettingApp and are not started anymore.
- ? - MarketDetailsDao is used in BettingEngine in BetsStat dao - break this dependency.
- 3 - Add overall status for all beans to the web console header. OK/FAILURE.
- 13 - When amount of markets analyzed by bot is limited to 1, then for each iteration the same market should be analyzed (There is no need to execute getMarkets()). 
  Also market closer to market time should be analyzed more often.
- bet sometimes is matched twice in two portions - how does it affect bot strategy?
- 5 - Put to the database CompleteMarketsCache
- 3 - StateMachineManager parses state machine file for every new market runner. Is it ok?

- 3 - Add state filter to bets module in console
- 5 - Console - add bets to market details.
- ? - Create facade module / Refactor console to use facade.
Fix virtual exchange and virtual console
	- 13 - Support multiples state machines in virtAccountStatementFacade/virtualActions/virtualExchange.
	- 1 - Statement module on virtual exchange doesn't work, null,null is passed to: new AccountStatementPanel.
	- 1 - Bets module on virtual exchange doesn't work, nulll is passed to: new BetsModule.
	- 34 - Split bf machine from virtual machine - two separate machine files.
	- 8 - Merge both business logic, there is no need for placeBet and placeVirtBet. They should be the same and the business logic too. 
	
COULD:
- Integration with betting exchanges, e.g. betdaq, www.sportingindex.com
- Console: When server is down and user clicks a new tab or chooses new value from drop down list then no action is taken and no error message is displayed.
- Replace reconcileVirtMarkets task with a listener - reconcile once when market is turn in play.
- Check why in marketDetails the sport: soccer is added (in addition to the SOCCER) and create the BetFairSportEnum
- refactor BetFirBwinRegionEnum: getSportName, getRegionName - the menuPath param is strange.
- When betfair markets or bwin service is down, then for the next 15 mins new soccer markets are not analyzed.
- Add max available mem to web console stat.
- Modify winner generator to use last prices before market is turn in play.
- Add console module to show context variable for runner.
- lastVirtBet.priceMatched/sizeMatched is set incorrectly (not consistent with lastBet.....)
- Add liability and betCategory to lastBet in db.
- Modify winner generator to generate winner on a market with more than one winner (placed market).
- Also add the last available priceToBack,priceToLay (before market turns in-play (charts with history).
- add isCancelled field to lastBet, also change machine.xml (maybe remove sizeCancelled)
- In the BWinMarket there are Betfair market names - move it somewhere else
- 1 - Display flexibet version in web console.
- 5 - Break dependency between webconsole and betfairservice - put AccountFunds to the database.
- 5 - Support multiple state machines in birt reports (State_Period, Sport_State_Period).

WOULD:
- The betId for virtBet is 'noLastBet' after bot restart, therefore cancelBet fails when parsing betId with classCastException String > Number.
- Add the BIRT_HOME to the BotConfig.
- Change ActionTester to set context variables not using MarketRunnerCtxHelper.
  Some variables are not tested in PlaceSPBet when passed to lastBetDAO.addLastBet, 
  e.g. price and priceErr.
- Data fix statement items are not added to database.
- Add to runner context: LASTBET_LAY_LIABILITY and LASTBET_BACK_LIABILITY.
- Add to runner context: LASTVIRTBET_LAY_LIABILITY and LASTVIRTBET_BACK_LIABILITY.
- Use the same date formatter around web console.
- Production/Test mode should be reconsidered when web console and server app are separated. 
- last run on stats show last successfull run - not the last failed run (it's useful information too)
- 28/03/2009 13:03:02 ERROR PlaceBetCommand - placeBet: BET_IN_PROGRESS (bet error:BET_IN_PROGRESS), price:3.89,validated price: 3.85, validated size: 4
- Implement RUNNER_ISGREEN context variable.
- Check if the same action instance is used(or not) for all executions.
- Monitor situation when state machine is removed and then added again for the same runner.
- ScxmlService uses classes from BotRunner. Break this dependency.
- All operations in fire event (add bet to db, set runner state MUST be a part of the same transaction).
- Create junit test for StateMachine (existing test is commented)
- Execution of one action can affect execution of next one (on the same market or the same runner).
  For instance the next one action doesn't know that the first one placed a bet. The new state of the markets should be
  visible for the second action. 
- LastVirtBet size in runner conxtex is always 0 , avgPriceMatched = price, etc. Is it a problem? It's because currently all bets on betting exchange are matched immediately and they are never canceled, 
  but if betting exchange is changed to not match immediately, then the runner context must be changed to.
- Use Joda time in VirtualDashboard to calculate beginning of week.
- Do not use the assembly/dist as a BOT_HOME.
- Bot started in devel mode should use botdbtest instead of botdb.
- Commission in account statement is assigned to any bet on a market instead to the one who gave the biggest profit.  Then some statistics may be not accurate e.g. for the hr_lh_layMatched
- Review exception handling - some important exceptions are not visible
- replace TODO stuff for horseracing with production code
- make all timer tasks (and all services) thread-safe.
- RunnerServiceTask is not safe, also if last executions are failed then there is no info how old is the date displayed on the web console (for the runnersSummary)
- startDate in account statement is wrong sometime (2003 year)
- put error, warnings (exceptions) to the database, separate network exceptions from other exceptions.
- change the price param to the bsbLiability for the starting price, change the startingPrice param to the betCategory (with default=E).
- Do the MarketStatHelper junit test.
- add to bot config Match Odds(Listed) for baseball
- remove BetFair exception or change it to runtime (update custom actions) if changed to runtime - remove try catch)
- turn the file logging off for the machine tester
- getMUBets - update in db only last bets (not all of them as now). It's done - check the performance (many findLastBet methods are executed)
- Check required botConfig parameters - must exist. Extend BotConfig to check required parameters and not null values for CustonAction and MarketFilter.
- services uses BotException and other stuff too - there are not isolated - check it
- analyze BetfairException in RunnerActions/Conditions
- analyze betFair.cancelBet (REMAINING CANCELED) and placeBet (checking results)
- What to do with a runner if performRunner is finished with an exception, e.g. updateRunnerState in db failed. Should this runner be analyzed again for the next bot execution. How about the rollback?
- Check ContextVariableEnum against null pointer exception, e.g. getRegion can be null (maybe set regionUnknown if no region)
- Move ThreadPoolTaskExecutor to spring file. Currently it's embedded inside OddsChecker and maybe other beans. Do the same with HttpClient.
- BIRT - show sports(regions) for def_states.
- BIRT - show profit for totalAmountMatched for runner and other from last_bet_runner.
- BIRT - show profit per market_name (from account statement, e.g. to be placed)
- BIRT - show total profit/amount of runners/markets over the time
- Stats: - p&l per bet type, numOfWinners, lastBackBetSize, per totalMatched (market/runner) when lastBackBet was placed. 
	 - green markets/runners per lastBackBetSize,
- 3 - Support RunnerStateCtxFactory in StateMachineTester.
- 3 - MARKET_ISGREEN and RUNNER_ISGREEN are not runnerstate specific.
- 8 - Split server and console application.


Check periodically:
- check account records in db against account records on betfair (sql is on the pulpit)
- Improve botrunner execution time (make it shorter).
- Check for memory usage.

****************************************************************************************************
Machine ideas:
A large volume customer can simply speculate the prices and make profits: buy
all high odds, lay on lower odds and this way an arbitrage opportunity occurs regardless
of the game result.
- Recognize markets where margin between back and lay is big only because someone matched lay or back back.
-  Check what is the backBetSize for backMatched runners. E.g. if it's low or high, maybe someone is trying to make the bets shorter?
- Set maxPrice for back bets,when priceToLay=1000 (or is very big), set Max back bet price (layPrice + ?%)
- Try to match back bet even if it's parts will be matched on different prices. Currently only the first part of back bet is matched.
- How to analyze markets during the one hour before market is started. E.g. currently runnerService obtains markets from marketCache which can be 15 mins delayed.


Machine ideas for later:
- http://www.sciencedirect.com/science?_ob=ArticleURL&_udi=B6VCT-4S32NMK-1&_user=10&_rdoc=1&_fmt=&_orig=search&_sort=d&view=c&_acct=C000050221&_version=1&_urlVersion=0&_userid=10&md5=c1e13cfa5aaa0e2a40439540e89427e8

- IRE: always lose at: hr_ire_backMatched, hr_ire_backMatched. Why? Maybe try to place oposite bets?

```