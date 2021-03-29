## 1. Objective
This fork introduces unit tests meant to test the isolated functionality of "earnings" in base.py lines 393 to 404.
For each problem identified by these new tests, our team will engage in and document one of the following responses:

1. Identify a pull request that solves the issue.
2. Implement, test, document, and merge via pull request a quick fix that solves the issue.
3. Document why the fix is too difficult to implement.

## 2. Team Members
1. Yimage Addus <br>
2. Ramjay Sarma <br>
3. Maristella Jho <br>
4. Abdul Hafiz Salifu <br>
5. Jacob Bakker 

## 3. Problems Encountered During Research Phase
- Missing fundamental data #547
    - Given specific dataset assert that cashflow, balance_sheet, financials etc. returns the expect result
- Incorrect revenue for some stocks #543
    - Assert that returned revenue value is the expected value
- Unable to get quarterly_financials #533
    - Assert that there is no errors thrown when attempting to retrieve quarterly_financials
- Financial Data not fetched #489
    - Given a specific dataset assert that financial data returns the expected financial data frame
- Empty data frame is returned for earnings, cashflow, balance sheet and financials #475
    - Given data assert that cashflow, balance_sheet, financials etc. don't return empty
- Problem with requesting asset.info for certain assets whilst other data fields like history are defined #448
    - Assert that the financials url is the expected value
- New issues on retrieving financial statement data #423
    - Assert that finance returns the expect financial statement data (.financials) from several sources (2 is enough)
- Financials information and more attributes are empty #419
    - Assert that finance returns a non empty dataframe (.financials) from several sources (2 is enough)
- Empty DataFrame for any financial related data #350
    - Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- Can't get cashflow data back #328
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- For the guys who successfully load balance sheet by patching the package, how to find the base.py? #292
    - Not sure this can be tested
- Cannot retrieve financial data from yfinance (with img) #291
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- Unable to get balance sheet and for all tickers - Module down? #254
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- Error when calling get_earnings() ect. #223
    - Assert that no errors are thrown when calling get_earnings()
- Proxy problem #213
    - Test using requests.get() on other websites
- Income Statement, Balance Sheet and Cashflows are coming up as an empty dataframe #191
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- Earnings and other financial information now being populated #181
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- KeyError: 'financialsChart' #173
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- Error when using ticker.info #150
    - (Duplicate)Assert that .financials, .quarterley_financials, .balance_sheet etc. return non empty dataframes
- Premium Yahoo finance #120
    - Assert that yahoo finance is not operating on the premium version

## 4. Planned Tests
Due to time constraints, we will only be implementing 3 unit tests to demonstrate how this testing approach can be applied to the base.py "earnings" section.<br>
The following three tests will be implemented:
| Test | Purpose | Issues Tested |
|------|--------|---------|
|1| Verify that self._earnings has the "yearly" key set to the appropriate dataframe generated from the data object.| |
|2| Verify that self._earnings has the "quarterly" key set to the appropriate dataframe generated from the data object.| |
|3| Verify that self._earnings has the "yearly" and "quarterly" keys set to their appropriate dataframes generated from the data object.| |

## 5. Risks
| Risk | Impact | Trigger | Mitigation Plan |
|------|--------|---------|-----------------|
|Uncaught side effects from leftover code in _get_fundamentals() method | High | If or try blocks that haven't been disabled | Deliberately leave certain object fields and data entries blank to prevent all non-earnings blocks from executing meaningful code. |

## 6. Test Approach
We intend to test the base.py "earnings" functionality by first isolating it from the rest of the _get_fundamentals() method.<br><br>
This method largely consists of several if blocks which execute if the data object contains a dictionary associated to a certain key (e.g. if isinstance(data.get('esgScores'), dict)). These blocks will be prevented from executing by ensuring that the data object does not contain any data at keys other than "earnings". Since the data object is provided
by the get_json() method of utils, a stub data object will be provided by a mock of get_json().<br><br>
All events will be skipped by simply not instantiating their required object fields. Since the events will execute a single pass call in the event of an exception, each event's first required class attribute will be set to None to force an exception.


## 7. Test Environment
Tests will be performed on one of our team members local machines running one of Windows, Mac OS, or Linux.
