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
<key>NSAppTransportSecurity</key>
<dict>
  <!--Include to allow all connections (DANGER)-->
  <key>NSAllowsArbitraryLoads</key>
      <true/>
</dict>

