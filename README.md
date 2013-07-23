#highscore
=========

Parse a log4j file to find the most common errors.

    [you@server:~/highscore]$ ./highscore  --lines=all --no-spinner --errorlevel=WARN --application=shopcart --logfile=friday-prod.log --resultcount=20
    parsing 28257 lines: done
    Let's lets look at the top 20 errors in all lines in friday-prod.log ...
    PLACE   SCORE   TYPE      NAME
    -----------------------------------------------------------------------------------
       1)     481   SEVERE  <span style="color:green">[com.example.crm.shopcart.servlet.SessionListener]</span> (ContainerBackgroundProcessor[StandardEngine[jboss.web]]) Error setting transaction state after session expired.: java.lang.NullPointerException
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
      12)      21   SEVERE  [com.example.crm.shopcart.biz.ItemBO] __AJP__ Failed GIF call for __BIN__: com.example.crm.shopcart.exception.GIFServiceException: Error retrieving vehicle data from GIF Service for:  __BIN__ userName: example_com 
      13)      17   SEVERE  [com.example.crm.shopcart.action.ErrorAction] __AJP__  
      14)       6   ERROR  [com.opensymphony.xwork2.interceptor.ExceptionMappingInterceptor] __AJP__ null: java.lang.NullPointerException
      15)       3   SEVERE  [com.example.crm.shopcart.action.ajax.WidgetInitAjaxAction] __AJP__ [__JSESSIONID__] FAILED TO CREATE ITEM! - Cannot sell this item.
      16)       2   ERROR  [com.opensymphony.xwork2.interceptor.ExceptionMappingInterceptor] __AJP__ WidgetInit ajax action was called before the session objects were available. Session size is: 0: java.lang.Exception: WidgetInit ajax action was called before the session objects were available. Session size is: 0
      17)       2   WARN  [org.jboss.jca.core.connectionmanager.pool.strategy.OnePool] __AJP__ IJ000612: Destroying connection that could not be successfully matched: org.jboss.jca.core.connectionmanager.listener.NoTxConnectionListener__MEMAREA__[state=DESTROYED managed connection=org.jboss.jca.adapters.jdbc.local.LocalManagedConnection__MEMAREA__ connection handles=0 __LASTUSE__ trackByTx=false pool=org.jboss.jca.core.connectionmanager.pool.strategy.OnePool__MEMAREA__ pool internal context=SemaphoreArrayListManagedConnectionPool__MEMAREA__[pool=SHOPCART]]
      18)       1   SEVERE  [com.example.crm.shopcart.biz.ItemBO] __AJP__ Failed PRDS call for __BIN__: java.lang.Exception: Unable to get vehicle data for __BIN__
      19)       1   ERROR  [com.opensymphony.xwork2.interceptor.ExceptionMappingInterceptor] __AJP__ java.lang.reflect.InvocationTargetException: org.apache.struts2.json.JSONException: java.lang.reflect.InvocationTargetException
      20)       1   SEVERE  [com.example.crm.shopcart.action.ajax.WidgetInitAjaxAction] __AJP__ [__JSESSIONID__] FAILED TO CREATE ITEM: java.lang.NullPointerException
    Ran in 1 second seconds.

