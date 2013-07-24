#highscore

**Parse a log4j file to find the most common errors.** Parser works by using customs regexes to tokenize common patterns in order to better identify "near idntical" errors. This may include datestamps, JSessionIDs, ip:port combinations, or memory addresses. Regexes are completely customizable by application.  Highscore has recently been rewritten to work with the default log formatting for JBoss EAP 6.0.1, so your mileage may vary.




    [you@server:~/highscore]$ ./highscore --help

    Usage: highscore [OPTION]...

        --application=APPNAME   Name of the application that produced the log; matching config file will try to load.
        --errorlevel=ERROR      Lowest log level to pay attention to; e.g. WARN lists WARN, SEVERE, ERROR and FATAL
        --logfile=LOG           Location of the logfile you wish to parse.           
        --lines=LINECOUNT       The number of lines from the bottom of the file that you wish to parse.
        --resultcount=COUNT     The number of results to show in the resulting table
        --no-spinner            Disable the text spinner showing process completion
        --no-color              Disable the syntax highlighting
        --help                  Display this help.



##An Example
So why use highscore? People never look at their logs. Logs are boring- especially log4j logs with 5 page stacktraces.
Lets look at an example from an actual production site for a former employer:



    [you@server:~/highscore]$ ./highscore  --lines=all --no-spinner --errorlevel=WARN --application=shopcart --logfile=friday-prod.log --resultcount=20
    parsing 28257 lines: done
    Let's lets look at the top 20 errors in all lines in friday-prod.log ...
    PLACE   SCORE   TYPE      NAME
    -----------------------------------------------------------------------------------
       1)     481   SEVERE  [com.example.crm.shopcart.servlet.SessionListener] (ContainerBackgroundProcessor[StandardEngine[jboss.web]]) Error setting transaction state after session expired.: java.lang.NullPointerException
       2)      74   SEVERE  [com.example.crm.shopcart.action.ErrorAction] __AJP__ __JSESSIONID__ 
       3)      68   WARN  [org.apache.fop.apps.FOUserAgent] __AJP__ Line 1 of a paragraph overflows the available area by __MILLIPOINTS__ (No context info available)
       4)      43   WARN  [org.jboss.jca.adapters.jdbc.local.LocalManagedConnectionFactory] __AJP__ Destroying connection that is not valid, due to the following exception: com.mysql.jdbc.JDBC4Connection__MEMAREA__: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure
       5)      41   WARN  [org.jboss.jca.core.connectionmanager.pool.strategy.OnePool] __AJP__ IJ000612: Destroying connection that could not be successfully matched: org.jboss.jca.core.connectionmanager.listener.NoTxConnectionListener__MEMAREA__[state=DESTROYED managed connection=org.jboss.jca.adapters.jdbc.local.LocalManagedConnection__MEMAREA__ connection handles=0 __LASTUSE__ trackByTx=false pool=org.jboss.jca.core.connectionmanager.pool.strategy.OnePool__MEMAREA__ pool internal context=SemaphoreArrayListManagedConnectionPool__MEMAREA__[pool=TAX]]
       6)      29   ERROR  [org.apache.catalina.core.ContainerBase.[jboss.web].[default-host].[/SHOPCART].[jsp]] __AJP__ Servlet.service() for servlet jsp threw exception: The Struts dispatcher cannot be found.  This is usually caused by using Struts tags without the associated filter. Struts tags are only usable when the request has passed through its servlet filter, which initializes the Struts dispatcher needed for this tag. - [unknown location]
       7)      28   SEVERE  [com.example.crm.shopcart.action.ErrorAction] __AJP__ ErrorAction: session was null or empty in Prepare()
       8)      27   SEVERE  [com.example.crm.shopcart.action.ajax.WidgetInitAjaxAction] __AJP__ [__JSESSIONID__] FAILED TO CREATE ITEM: java.lang.Exception: Invalid Example.com Internet Price of 0.00 for __BIN__
       9)      26   SEVERE  [com.example.crm.shopcart.action.ajax.TradeinAjaxAction] __AJP__ [__JSESSIONID__] ymmtbLists FAILED: com.example.crm.shopcart.exception.TradeinServiceException: __GET_BODY_STYLES__
      10)      24   SEVERE  [com.example.crm.shopcart.servlet.SessionListener] __AJP__ Error setting transaction state after session expired.: java.lang.NullPointerException
      11)      22   SEVERE  [com.example.crm.shopcart.action.ajax.WidgetInitAjaxAction] __AJP__ [__JSESSIONID__] FAILED TO CREATE ITEM: com.example.crm.shopcart.exception.FailedToCreateItemException: Item was not found in the current inventory.
      12)      21   SEVERE  [com.example.crm.shopcart.biz.ItemBO] __AJP__ Failed GIF call for __BIN__: com.example.crm.shopcart.exception.GIFServiceException: Error retrieving vehicle data from GIF Service for:  __BIN__ userName: example_com password: redacted Service_URL: http://example.com/service2/something
      13)      17   SEVERE  [com.example.crm.shopcart.action.ErrorAction] __AJP__  
      14)       6   ERROR  [com.opensymphony.xwork2.interceptor.ExceptionMappingInterceptor] __AJP__ null: java.lang.NullPointerException
      15)       3   SEVERE  [com.example.crm.shopcart.action.ajax.WidgetInitAjaxAction] __AJP__ [__JSESSIONID__] FAILED TO CREATE ITEM! - Cannot sell this item.
      16)       2   ERROR  [com.opensymphony.xwork2.interceptor.ExceptionMappingInterceptor] __AJP__ WidgetInit ajax action was called before the session objects were available. Session size is: 0: java.lang.Exception: WidgetInit ajax action was called before the session objects were available. Session size is: 0
      17)       2   WARN  [org.jboss.jca.core.connectionmanager.pool.strategy.OnePool] __AJP__ IJ000612: Destroying connection that could not be successfully matched: org.jboss.jca.core.connectionmanager.listener.NoTxConnectionListener__MEMAREA__[state=DESTROYED managed connection=org.jboss.jca.adapters.jdbc.local.LocalManagedConnection__MEMAREA__ connection handles=0 __LASTUSE__ trackByTx=false pool=org.jboss.jca.core.connectionmanager.pool.strategy.OnePool__MEMAREA__ pool internal context=SemaphoreArrayListManagedConnectionPool__MEMAREA__[pool=SHOPCART]]
      18)       1   SEVERE  [com.example.crm.shopcart.biz.ItemBO] __AJP__ Failed PRDS call for __BIN__: java.lang.Exception: Unable to get vehicle data for __BIN__
      19)       1   ERROR  [com.opensymphony.xwork2.interceptor.ExceptionMappingInterceptor] __AJP__ java.lang.reflect.InvocationTargetException: org.apache.struts2.json.JSONException: java.lang.reflect.InvocationTargetException
      20)       1   SEVERE  [com.example.crm.shopcart.action.ajax.WidgetInitAjaxAction] __AJP__ [__JSESSIONID__] FAILED TO CREATE ITEM: java.lang.NullPointerException
    Ran in 1 second seconds.


(it's color coded on the command line, I promise.)

So what can we learn from this simplification?

* The original file was 28k lines.
* line 1: That null pointer exception happened 481 times in one day. Caused by poor handling of inconsistent data, this accounted for most of the logs.
* line 4: something is not closing database connections properly. This could be a problem under load.
* line 6: a struts error that may be manifesting ugliness to your users
* line 8: pricing consistency error is revealed for some items
* line 12: connection to 3rd party service failed and then wrote a password to the log file (!)
* The entire parsing of the 28k file took one second.


## Tuning

The first time you run highscore, you may see several entries that look near identical:

       17)      1   WARN  [org.apache.fop.apps.FOUserAgent] __AJP__ Line 1 of a paragraph overflows the available area by 11253 millipoints (No context info available)
       18)      1   WARN  [org.apache.fop.apps.FOUserAgent] __AJP__ Line 1 of a paragraph overflows the available area by 23934 millipoints (No context info available)
       19)      1   WARN  [org.apache.fop.apps.FOUserAgent] __AJP__ Line 1 of a paragraph overflows the available area by 11395 millipoints (No context info available)
       20)      1   WARN  [org.apache.fop.apps.FOUserAgent] __AJP__ Line 1 of a paragraph overflows the available area by 19578 millipoints (No context info available)

By adding a new regex to the configuration (something like line 2):

    [Replacements]
        1 >>SEARCH_TERM<<        = bogusresultthatwontmatch
        2 >>MILLIPOINTS<<        = \d+ millipoints\.

You should see a all of those near identical errors "stack". Suddently your minor annoyance is the 3rd most common error in the logfile

       3)      68   WARN  [org.apache.fop.apps.FOUserAgent] __AJP__ Line 1 of a paragraph overflows the available area by __MILLIPOINTS__ (No context info available)


