# robinhood-python
Robinhood module in Python

Some current caveats:
* Development has been in python 3, I'm not taking much care to keep python 2 support at the moment.
* The scripts currently default to extreme caching policies, use --live to guarantee most recent data.
* Much of the code will assert (or not) in scenarioes where states and paging is involved where they haven't been handled correctly yet

## Security

* Certificate pinning is used to block against MITM attacks

## Module

* [RobinhoodClient](robinhood/RobinhoodClient.py)
  * Client that handles getting data from the Robinhood APIs
* [RobinhoodCachedClient](robinhood/RobinhoodClient.py)
  * Client that handles caching on top of the normal client

## Scripts

* [login.py](login.py)
  * Forces a new login and caches the token. Note most scripts will do this
    automatically so you usually don't need to call this.
* [logout.py](logout.py)
  * Invalidates the current auth token and deletes the cached token

Various downloads:
* [download_portfolio.py](download_portfolio.py) [--live]
  * Current positions with various stats
* [download_history.py](download_history.py) [--live]
  * Downloads all account history (orders, dividends, transfers, rewards, margin, etc.)
* [download_documents.py](download_documents.py) [--live]
  * Documents (including PDFs) that you've received

Display information:
* [show_quote.py](show_quote.py) AMZN [--live]
  * Displays the latest stock quote for the given symbol along with auxilary info
* [show_options_quote.py](show_options_quote.py) [call|put] AMZN 2018-05-21 55 [--live]
  * Displays the quote for the given options contract (pretty raw for now)
* [show_pending_orders.py](show_pending_orders.py)
  * Displays any outstanding stock orders along with position information
* [show_interesting_stocks.py](show_interesting_stocks.py)
  * Show stocks that are on various lists
    * 10 popular S&P 500 stocks with Robinhood users
    * S&P 500 top movers up and down
    * Top 10 and 100 popular sticks with Robinhood users
  * This script is kind of a mess and mostly just a raw dump.
* [show_potentials.py](show_potentials.py)
  * Show stocks and some stats to help decide on positions to push forward on.
    * Note this is basically only useful to myself ATM.

Perform actions:
* [order.py](order.py) [market|limit] [buy|sell] SYMBOL QUANTITY PRICE [--no-cancel]
  * Prints the quote for the given symbol, confirms, and places an order
* [cancel.py](cancel.py) ORDER_ID...
  * Cancels one or more order ids given, or all pending orders if none given
* [cancel_options.py](cancel_options.py) ORDER_ID...
  * Cancels one or more options order ids given, or all pending options orders if none given

## Legal

* This library may have bugs which could result in financial consequences, you are responsible for anything you execute. Inspect the underlying code if you want to be sure it's doing what you think it should be doing.
* I am not affiliated with Robinhood and this library uses an undocumented API. If you have any questions about them, contact Robinhood directly: https://robinhood.com/
* By using this library, you understand that you are not to charge or make any money through advertisements or fees. Until Robinhood releases an official API with official guidance, this is only to be used for non-profit activites.  I am not responsible if Robinhood cancels your account because of misuse of this library.
