Appunti
=======
####Export Android
source ~/.bash_profile

##### Hide Status Bar IOS
##### Aggiungere queste due righe al file .plist

```
 <key>UIStatusBarHidden</key>
<true/>
<key>UIViewControllerBasedStatusBarAppearance</key>
<false/> 


```

https://github.com/devgeeks/ExampleHTML5AudioStreaming




---------


Allow connessione esterne

```
<key>NSAppTransportSecurity</key>
<dict>
  <!--Include to allow all connections (DANGER)-->
  <key>NSAllowsArbitraryLoads</key>
      <true/>
</dict>
```


-------


```
- (BOOL)webView:(UIWebView *)theWebView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)­navigationType
{ NSURL *url = [request URL]; // Intercept the external http requests and forward to Safari.app // Otherwise forward to the PhoneGap WebView if ([[url scheme] isEqualToString:@"http"] || [[url scheme] isEqualToString:@"https"]) { [[UIApplication sharedApplication] openURL:url]; return NO; } else { return [ super webView:theWebView shouldStartLoadWithRequest:request navigationType:navigationType ]; }
}


```

//https://www.youtube.com/watch?v=zqbjXSnAR-Q
pwd

