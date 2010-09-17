Lua OAuth
=========

A Lua client library for OAuth 1.0 enabled servers.

This is an adaptation of Jeffrey Friedl's [Twitter OAuth Authentication Routines in Lua, for Lightroom Plugins][1], 
with Lightroom's code replaced by other libraries (i.e. [LuaSec][2], [LuaSocket][3], etc) and with HMAC-SHA1 calculations 
done with [LuaCrypto][4] instead of [plain Lua][6]

Most of the code was taken from [Jeffrey Friedl's blog][1]

Usage
=====
You can take a look at the unit tests. For instance, the file ''unittest/echo_lab_madgex_com.lua'' creates a client that 
uses the test service provided by [madgex.com][5].

Basically, you create an OAuth client with your consumer key and secret, providing the OAuth service's endpoints URLs (i.e. 
where to request a token, where to get an access token, etc).

    local OAuth = require "OAuth"
    local client = OAuth.new("key", "secret", {
    	RequestToken = "http://echo.lab.madgex.com/request-token.ashx", 
    	AccessToken = "http://echo.lab.madgex.com/access-token.ashx"
    })

Now you can request a token and then an access token:
    local values = client:RequestToken()
    values = client:GetAccessToken()

Once you have been authorized, you can perform requests:
    local code, headers, statusLine, body = client:PerformRequest("POST", "http://echo.lab.madgex.com/echo.ashx", {status = "Hello World From Lua (again)!" .. os.time()})


[1]: http://regex.info/blog/lua/twitter
[2]: http://www.inf.puc-rio.br/~brunoos/luasec/
[3]: http://w3.impa.br/~diego/software/luasocket/
[4]: http://luacrypto.luaforge.net/
[5]: http://echo.lab.madgex.com/
[6]: http://regex.info/blog/lua/sha1