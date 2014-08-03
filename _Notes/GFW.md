---
layout: indexed
title: 網絡原貌大作戰
date: 2011/03/19 02:03:47
---
2011.03.19 作， 2014.06.19 重寫。  
  
本文主要介紹某牆的運作方式及網上存在的繞過方法。這種牆包括但不限於我們熟知的 GFW ，他也廣泛應用於各公司、機構——比如 NTU ，就有一個叫 CITS 的東西，名義上是管理全校的網絡，實際上做了不少蠢事，比如把學校郵箱放到 live.com 上，還有禁止師生使用迅雷、優酷、土豆、 PPS 之類流量大的東西。甚至某些邪惡的網絡運營商員工還會利用這些技術來獲取不正當收入……  
本文不涉及任何下載，且是私人筆記。如果有人不懷好意的閱讀本文，請自插雙目。  
  
##DNS 的劫持與污染
DNS (Domain Name System) 簡單說來就是把域名「翻譯」（應該叫解析）成 IP 地址的系統。這個「翻譯」的過程如果有了貓膩，就像美國人說 I love you ，結果翻成「你去死」一樣。  
DNS 不能憑空翻譯，總要藉助某機器完成，如果有人在用戶和 DNS 服務器之間設牆，篡改解析的 IP 地址，那就是 DNS 劫持。效果是敲了淘寶，結果跑到掏包去了，我所在的電信就用這種辦法把京東劫持到他的聯盟上，每當用戶上京東買東西時，他就能獲取一些佣金。  
DNS 污染則是在劫持的時候直接給一個虛假的 IP ，結果用戶上了這個虛假 IP 發現網頁是空的，就以爲網站掛了。  
####使用良心 DNS
現在得到國際認可的就是 OpenDNS 和 Google DNS 。當然爲了本國網絡的速度，各國都會做這個。中國的當然都帶有污染，但好處是速度快——對於新裝系統，美國的 DNS 難免延遲較長。現在中國又有了個 OpenerDNS 是防污染的，不知道能撐多久。如果主要訪問國內網站，還是用 114 或阿里比較快。  
設置時，先在 TCP/IP 協議填寫他們提供的 IP ，但還是可能被污染劫持，這就需要跟瀏覽器打個招呼，堅決使用指定 DNS 不動搖。對於 FireFox ，在 about:config 修改 network.proxy.socks\_remote\_dns 爲 true 卽可。Chrome 默認帶這功能。  
####修改 hosts
如果我們直接告訴電腦域名應該解析成什麼 IP ，電腦就不會傻傻的再問高牆，或是遠赴美國問 Google 。這就需要設置 hosts 文件。由於不需要什麼跳板，我認爲這個可以算是穿牆。  
**SmartHosts** 提供若干常用被牆網站的眞實 IP ，比如 Google, Facebook, Dropbox 。  
**imouto.host** 在前者的基礎上屛蔽一些廣告。  
**HostsX** 記事本風格的 hosts 文件修改軟件，以前還帶有很頗豐富的數據庫，隨時更新常用被牆網站和廣告屛蔽。  
**huhamhire-hosts** HostsX的簡化+弱化版。  
**SwitchHosts** 顧名思義，如果有多份 hosts 文件，用他來切換很不錯。還能設置一些網址，隨時更新。  
**HostMan** 葡萄牙人製作，相當強大細緻，開發也很活躍，官網已牆。  
  
##關鍵字屛蔽
比如 GitHub ，就曾被關鍵字屛蔽過，域名包含 GitHub 的網站，一律不可訪問——就算 hosts 塡了正確的 IP 也不行。  
更嚴峻的關鍵字屛蔽是，不但域名包含關鍵字，而且網頁內容包含關鍵字，就會屛蔽。  
####不能屛蔽的網站
GFW 的關鍵字屛蔽很蠢，爲什麼說很蠢呢？比如中國日報的網站是 chinadaily.com.cn ，如果有人註冊一個域名，叫 adaily.co ，發佈色情內容，結果被 GFW 了，那中國日報也會遭殃……這樣其實 adaily.co 是不能屛蔽的。  
####HTTPS
HTTPS 帶了 SSL ，加密傳輸內容，本來主要是給銀行、郵箱之類需要加密的網站用。但加密後牆看到的就是一堆亂碼，就無法屛蔽了。這姑且叫騙牆。  
所以， https 結合一個肥碩的 hosts ，穿牆結合騙牆，是最高效訪問常用網站的方式。  
####Telex
Telex 會在一個正常訪問的網站請求上附加一個加密的標籤，標籤就是那個被屏蔽的網站。  
項目由密歇根大學提供，不過好多年不更新了。  
  
##封 IP
這是最嚴厲的方式，直接切斷用戶與服務器之間的聯繫。對於多如牛毛的小站，牆通常喜歡用這種直接快速的辦法。  
對付他，衹能找個沒有被屛蔽的中間人，然後通過這個中間人來跟服務器聯繫，這纔是眞正翻牆。  
####VPN
Virtual Private Network ，是個可以加密的、一般屬於小羣體的專用網絡。本來設計應用於機構內部，但現在也作爲翻越的主要方式。  
VPN 的缺點是，不管訪問什麼網站，都要先經過 VPN 的那個服務器。如果這個 VPN 是自己學校或公司還好，因爲近，不會延遲太久，但如果服務器遠在太平洋彼端，而自己又要訪問一個在此端的網站，那這數據得繞地球一圈，本來一百毫秒就到了，這下都一秒了。  
**OpenVPN** 現在最常用的一個服務器端的 VPN 。  
**chnroutes** 一個幫助 VPN 決定哪些網站直接訪問、哪些網站要翻的腳本，可減輕 VPN 壓力。  
####SSH
Secure Shell 與 VPN 相似，但好處是他並非全局的，設置代理了纔用遠程服務器，不設置還是本地網絡。  
由於該技術廣泛應用於服務器端的管理，很多虛擬空間都提供 SSH 服務，不用買 VPS ，服務器方面不需要安裝軟件，本地使用 MyEnTunnel, Bitvise SSH Client, PuTTY 等軟件卽可。  
####網頁代理
直接在瀏覽器上打開網頁代理，輸入想要訪問的網站卽可，好處是不用裝軟件。  
一般的虛擬空間都可以配置網頁代理，常見網頁代理有 APJP, phpsocks5, phproxy encrypt, KnProxy, PHP Tunnel Proxy, hyk-proxy 等。  
國內外很多高校的圖書館就利用 EZProxy 技術來提供校外訪問。  
####郵箱法
往某個特定的郵箱發一封郵件，在郵件的標題或正文包含你要訪問的 URL ，該郵箱會自動回信，信上就是訪問內容。  
####利用各種 PaaS
PaaS 可以理解爲限制使用特定語言的 VPS 。比如最著名的 GAE ，他原本就是單 Python 的。  
**GoAgent** 翻越界老大，支持 GAE 和 PHP 。  
**GAEProxy** GoAgent 的 Android 客戶端。  
**Wallproxy** 兼容 GoAgent 的客戶端，支持多線程和更多加密方式。  
**GreatAgent** 在 GoAgent 和 Wallproxy 的基礎上，更傻瓜的使用方式。  
**Snova** **GSnova** 支持多種 PaaS 的工具。  
**fqrouter** Android 客戶端，自帶跳板，同時支持 GoAgent/SSH/HTTP/SPDY/Shadowsocks 。  
**Shadowsocks** 輕量級代理，部署過程簡單，但需要一個具有 root 權限的 VPS 。  
####CDN
CDN 的本意是當用戶訪問一個離他比較遠的網站時，網站自動讓他訪問一個離用戶比較近的鏡像。但是這樣正好可以給我們用來翻越。  
不過現在高牆已經封掉了很多 CDN 提供商的 IP 。  
####反向代理
反向代理就是服務器通過另一臺服務器將自己的內容發佈到公網，當服務器的眞實 IP 被封後，如果使用一個未被封的 IP 作爲發佈方，就能翻越了。  
####P2P
基於 PaaS 或是其他服務器的翻越方式的缺點在於服務器的 IP 再多，終究不如全球普通用戶的 IP 多。  
**Tor** 由於被國內屏蔽中央目錄服務器，並不十分好用，但翻越後用來匿名倒是不錯的。  
**I2P** Tor 的進化版。 Tor 每次都需要連接中央目錄服務器以便接上其他用戶，而 I2P 祇需連接上第一次即可，以後都使用 Kad 連接。  
**uProxy** 華盛頓大學提供，未公開。