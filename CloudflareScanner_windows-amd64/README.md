# Ptechgithub/CloudflareScanner

[![Go Version](https://img.shields.io/github/go-mod/go-version/Ptechgithub/CloudflareScanner.svg?style=flat-square&label=Go&color=00ADD8&logo=go)](https://github.com/Ptechgithub/CloudflareScanner/)[![Release Version](https://img.shields.io/github/v/release/Ptechgithub/CloudflareScanner.svg?style=flat-square&label=Release&color=00ADD8&logo=github)](https://github.com/Ptechgithub/CloudflareScanner/releases/latest)[![GitHub license](https://img.shields.io/github/license/Ptechgithub/CloudflareScanner.svg?style=flat-square&label=License&color=00ADD8&logo=github)](https://github.com/Ptechgithub/CloudflareScanner/)[![GitHub Star](https://img.shields.io/github/stars/Ptechgithub/CloudflareScanner.svg?style=flat-square&label=Star&color=00ADD8&logo=github)](https://github.com/Ptechgithub/CloudflareScanner/)[![GitHub Fork](https://img.shields.io/github/forks/Ptechgithub/CloudflareScanner.svg?style=flat-square&label=Fork&color=00ADD8&logo=github)](https://github.com/Ptechgithub/CloudflareScanner/)

Many foreign websites are using Cloudflare CDN, but the IP assigned to visitors from mainland China is not friendly (high latency, high packet loss, and slow speed).  
While Cloudflare exposes all [IP segment](https://www.cloudflare.com/ips/), but trying to find one that suits you among so many IPs would be exhausting, so I came up with this software.

**"Self-selected preferred IP" tests Cloudflare CDN latency and speed to obtain the fastest IP (IPv4+IPv6) **! If it's useful**Click`⭐`Give me some encouragement~**

* * *

### Quick to use

### Download and run

1.  Download the compiled executable file [Github Releases](https://github.com/Ptechgithub/CloudflareScanner/releases) and unzip it.
2.  Double click to run`CloudflareScanner.exe`File (Windows system), waiting for the speed test to complete...

<details>
<summary><code><strong>「 Click to view usage examples on Linux system 」</strong></code></summary>

* * *

The following commands are only examples. For the version number and file name, please go to [**Releases**](https://github.com/Ptechgithub/CloudflareScanner/releases) Check.

```yaml
# If this is your first time using it, it is recommended to create a new folder (skip this step for subsequent updates)
mkdir CloudflareScanner

# Enter the folder (for subsequent updates, only repeat the following download and unzip commands from here)
cd CloudflareScanner

# Download the CloudflareScanner zip file (replace [version number] and [file name] in the URL according to your needs)
wget -N https://github.com/Ptechgithub/CloudflareScanner/releases/download/v2.2.5/CloudflareScanner_linux_amd64.zip
# If you are downloading in a Chinese network environment, please use one of the following mirror accelerations:
# wget -N https://download.scholar.rr.nu/Ptechgithub/CloudflareScanner/releases/download/v2.2.5/CloudflareScanner_linux_amd64.zip
# wget -N https://ghproxy.cc/https://github.com/Ptechgithub/CloudflareScanner/releases/download/v2.2.5/CloudflareScanner_linux_amd64.zip
# wget -N https://ghproxy.net/https://github.com/Ptechgithub/CloudflareScanner/releases/download/v2.2.5/CloudflareScanner_linux_amd64.zip
# wget -N https://gh-proxy.com/https://github.com/Ptechgithub/CloudflareScanner/releases/download/v2.2.5/CloudflareScanner_linux_amd64.zip
# wget -N https://mirror.ghproxy.com/https://github.com/Ptechgithub/CloudflareScanner/releases/download/v2.2.5/CloudflareScanner_linux_amd64.zip
# If the download fails, try removing the -N parameter (if for updating, remember to delete the old zip file in advance rm CloudflareScanner_linux_amd64.zip)

# Unzip (no need to delete old files, they will be overwritten directly, replace the file name according to your needs)
tar -zxf CloudflareScanner_linux_amd64.zip

# Grant execution permission
chmod +x CloudflareScanner

# Run (without parameters)
./CloudflareScanner

# Run (with parameter example)
./CloudflareScanner -dd -tll 90
```

> If flat**Very low latency**(such as 0.xx), then CloudflareScanner**The agent left during the speed test**, please close the proxy software before testing the speed.  
> if in**router**It is recommended to turn off the proxy in the router first (or exclude it), otherwise the speed test results may be**Inaccurate/unusable**。

</details>

* * *
> Notice! This software only works on websites,**Preferred IP for Cloudflare WARP is not supported**, see for details:[#392](https://github.com/Ptechgithub/CloudflareScanner/discussions/392)

### Example of results

After the speed test is completed, it will be displayed by default**Fastest 10 IPs**, example:

```bash
IP Address      Sent  Received  Loss-Rate  Avg-Latency  Download Speed (MB/s)
104.27.200.69     4       4       0.00         146.23    28.64
172.67.60.78      4       4       0.00         139.82    15.02
104.25.140.153    4       4       0.00         146.49    14.90
104.27.192.65     4       4       0.00         140.28    14.07
172.67.62.214     4       4       0.00         139.29    12.71
104.27.207.5      4       4       0.00         145.92    11.95
172.67.54.193     4       4       0.00         146.71    11.55
104.22.66.8       4       4       0.00         147.42    11.11
104.27.197.63     4       4       0.00         131.29    10.26
172.67.58.91      4       4       0.00         140.19    9.14
...

# If the average latency is very low (e.g., 0.xx), it indicates that CloudflareScanner is using a proxy during the speed test. Please disable any proxy software before conducting the test.
# If running on a router, please disable any proxies within the router (or exclude them), otherwise the speed test results may be inaccurate/unusable.

# Because each speed test randomly selects an IP from each IP range, the results will vary each time, which is normal!

# Note! I found that after the computer boots up, the first speed test may have noticeably higher latency (manual TCPing is the same), but subsequent tests are normal.
# Therefore, it is recommended that before conducting the first official speed test after booting up, randomly test a few IPs (no need to wait for the latency test to complete, just close it once the progress bar moves).

# The entire process of the software under the default parameters:
# 1. Latency test (default TCPing mode, HTTPing mode requires manual addition of parameters)
# 2. Latency sorting (sorting latency from low to high and filtering according to conditions, different loss rates are sorted separately, so there may be some IPs with low latency but loss at the end)
# 3. Download speed test (starting from the IP with the lowest latency, downloading speed tests one by one, the default stops after testing 10)
# 4. Speed sorting (sorting speeds from high to low)
# 5. Output results (control whether to output to the command line with parameters (-p 0) or output to a file (-o ""))

# Note: The result file result.csv will display Chinese garbled characters when opened with Microsoft Excel, which is normal. It displays normally in other spreadsheet software/notepad.
```

The first line of the speed test result is**The fastest IP with the fastest download speed and lowest average latency**！

The complete results are saved in the current directory`result.csv`file, use**Notepad/sheet software**Open, the format is as follows:

    IP Address, Sent, Received, Loss Rate, Average Latency, Download Speed (MB/s)
    104.27.200.69,4,4,0.00,146.23,28.64

> _You can view the complete results according to your own needs**Further filtering**, or take a look at the advanced usage**Specify filter criteria**！_

* * *

### Advanced use

The default parameters are used for direct operation. If you want the speed measurement results to be more comprehensive and more in line with your own requirements, you can customize the parameters.

```css
C:\>CloudflareScanner.exe -h

CloudflareScanner vX.X.X
Test the latency and speed of all IP addresses of Cloudflare CDN to obtain the fastest IP (IPv4+IPv6)!
https://github.com/Ptechgithub/CloudflareScanner

Options:
    -n 200
        Latency test threads; more threads result in faster latency testing, but devices with weak performance (such as routers) should not set it too high; (default 200, maximum 1000)
    -t 4
        Latency test count; number of times each IP's latency is tested; (default 4 times)
    -dn 10
        Download test count; number of IPs to download speed test after latency testing and sorting, starting from the lowest latency; (default 10)
    -dt 10
        Download test time; maximum download test time for each IP, should not be too short; (default 10 seconds)
    -tp 443
        Specify test port; port used for latency testing/download testing; (default port 443)
    -url https://cf.xiu2.xyz/url
        Specify test URL; URL used for latency testing (HTTPing)/download testing, default URL not guaranteed to be available, it is recommended to use a self-built one;

    -httping
        Switch test mode; switch latency test mode to HTTP protocol, using the test address specified by [-url] parameter; (default TCPing)
        Note: HTTPing is essentially a form of network scanning behavior, so if you are running it on a server, you need to reduce concurrency (-n), otherwise some strict merchants may suspend service.
        If you encounter a situation where the number of IPs available for HTTPing latency testing is normal at first, but decreases in subsequent tests or even becomes 0, but then recovers after a while, it may also be due to temporary restrictions triggered by the ISP or Cloudflare CDN due to network scanning behavior, it is recommended to reduce concurrency (-n) to reduce the occurrence of such situations.
    -httping-code 200
        Valid status codes; valid HTTP status codes returned when latency testing with HTTPing, limited to one; (default 200 301 302)
    -cfcolo HKG,KHH,NRT,LAX,SEA,SJC,FRA,MAD
        Match specified locations; location names are three-letter airport codes, separated by commas, case-insensitive, supports Cloudflare, AWS CloudFront, only available in HTTPing mode; (default all locations)

    -tl 200
        Upper limit of average latency; only output IPs with latency lower than the specified value, upper and lower limit conditions can be used together; (default 9999 ms)
    -tll 40
        Lower limit of average latency; only output IPs with latency higher than the specified value; (default 0 ms)
    -tlr 0.2
        Upper limit of loss rate; only output IPs with loss rate lower than/equal to the specified value, range 0.00~1.00, 0 filters out any IPs with loss; (default 1.00)
    -sl 5
        Lower limit of download speed; only output IPs with download speed higher than the specified value, will stop testing when the specified number [-dn] is reached; (default 0.00 MB/s)

    -p 10
        Number of results to display; directly display the specified number of results after testing, when set to 0, results will not be displayed and the program will exit directly; (default 10)
    -f ip.txt
        IP range data file; if the path contains spaces, please enclose it in quotes; supports other CDN IP ranges; (default ip.txt)
    -ip 1.1.1.1,2.2.2.2/24,2606:4700::/32
        Specify IP range data; directly specify the IP range data to be tested through parameters, separated by commas; (default empty)
    -o result.csv
        Write result to file; if the path contains spaces, please enclose it in quotes; set to empty [-o ""] to not write to file; (default result.csv)

    -dd
        Disable download speed test; after disabling, the test results will be sorted by latency (default sorted by download speed); (default enabled)
    -allip
        Test all IPs; test each IP in the IP range (IPv4 only); (default randomly test one IP from each /24 range)

    -v
        Print program version + check for updates
    -h
        Print help information
```

### Interface explanation

In order to prevent everyone from being concerned about the speed measurement process,**The output content is misunderstood (available, queue and other numbers, the download speed test is "interrupted" halfway?)**, I explain specifically.

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

> This example adds all common parameters, which is:`-ttl 40 -tl 150 -sl 1 -dn 5`, the final output result is as follows:

```bash
# Ptechgithub/CloudflareScanner vX.X.X

Starting latency test (mode: TCP, port: 443, range: 40 ~ 150 ms, loss: 1.00)
321 / 321 [----------------------------------------------------------------------------------] Available: 30
Starting download speed test (minimum: 1.00 MB/s, count: 5, queue: 10)
3 / 5 [---------------------------------------------------------↗---------------------------]
IP Address      Sent   Received Loss Rate  Avg Latency  Download Speed (MB/s)
XXX.XXX.XXX.XXX   4         4      0.00      83.32         3.66
XXX.XXX.XXX.XXX   4         4      0.00      107.81        2.49
XXX.XXX.XXX.XXX   4         3      0.25      149.59        1.04

Full test results have been written to the result.csv file, which can be viewed using Notepad/spreadsheet software.
Press Enter or Ctrl+C to exit.
```

* * *

> People who are new to CloudflareScanner may be confused**There are obviously 30 IPs available for delay speed testing, so why are there only 3 left in the end?**  
> What does the queue in the download speed test mean? Do I still have to queue up when I download the speed test?

CloudflareScanner will first delay the speed test, during which the number of available IPs will be displayed in real time on the right side of the progress bar (`Available: 30`), but note that the available quantity refers to**Number of IPs that passed the test without timeout**, has nothing to do with the upper and lower limits of delay and packet loss conditions. When the delayed speed test is completed, because it is also specified**Delay upper and lower limits, packet loss**conditions, so after filtering according to the conditions, only`10`Already (that is, waiting for the download speed test)`queue：10`）。

That is, in the above example,`321`After the IP delay speed test is completed, only`30`Each IP test passes without timeout, and then according to the upper and lower limit range of delay:`40 ~ 150 ms`and packet loss upper limit conditions, only`10`There is an IP that meets the requirements. if you`-dd`If the download speed test is disabled, this will be output directly.`10`IP. Of course, this example is not disabled, so the software will continue to`10`IP for download speed test (`queue：10`）。

> Because the download speed test is a single-threaded one-by-one IP queue test, so the number of IPs waiting for the download speed test is called`queue`。

* * *

> You may have noticed,**It was clearly designated to find 5 IPs that meet the download speed conditions, but why was it "interrupted" after only 3?**

Download speed test progress bar`3 / 5`, the former refers to finding`3`IPs that meet the lower limit of download speed (that is, the download speed is higher than`1 MB/s`),the latter`5`Refers to your request to find`5`IPs that meet the lower limit of download speed (`-dn 5`）。

> Also, a reminder, if you specify`-dn`is larger than the download speed test queue. For example, after you delay the speed test, only`4`IP, then the numbers behind the download speed test progress bar will be the same as the download speed test queue.`4`one, not you`-dn`Specified`5`Already.

The software is finishing the speed test`10`After IPs, only`3`download speeds higher than`1 MB/s`of IPs, and the rest`7`Each IP is "failed".

Therefore, this is not "Every time the speed test falls short of 5 it interrupts", but rather, all IPs have been downloaded and their speeds tested, yet only found `3` that meet the criteria.

* * *

If you don’t want to encounter this situation where few of the speed tests meet the conditions, then you have to**Lower the download speed limit parameter`-sl`**, or remove.

Because as long as you specify`-sl`parameters, then as long as there are not enough`-dn`number (default 10), the speed test will continue until enough or all speed tests are completed. Remove`-sl`and add`-dn 20`parameters, so that only the top 20 IPs with the lowest speed and delay are measured, and the speed measurement is stopped to save time.

* * *

In addition, if all queue IPs have been tested for speed, but there is no IP that meets the download speed conditions, then it will**Directly output the download speed test results of all queue IPs**, so that you can see the download speeds of these IPs, and you can know them in your mind, and then**Adjust it appropriately`-sl`try again**。

Similarly, in terms of delayed speed measurement,`Available: 30`、`queue：10`These two values ​​​​can also let you know whether the delay conditions you set are too harsh for you. If there are a lot of available IPs, but only 2 or 3 are left after conditional filtering, it goes without saying that you need**Adjust down expected latency/packet loss conditions**.

Of these two mechanisms, one tells you**Delayed packet loss conditions**Whether it is appropriate or not, one will tell you**Download speed conditions**Is it appropriate.

</details>

* * *

### Usage example

Windows To specify parameters you need to run in CMD, or add parameters to the shortcut target.

> **Notice**: Each parameter has**default value**, parameters using default values ​​can be omitted (**Choose as needed**),parameter**In no particular order**。  
> **hint**：Windows**PowerShell**Just put in the following command`CloudflareScanner.exe`Change to`.\CloudflareScanner.exe`That’s it.  
> **hint**: Linux system only needs to change the following command`CloudflareScanner.exe`Change to`./CloudflareScanner`That’s it.

* * *

#### #CMD runs CloudflareScanner with parameters

People who are not familiar with command line programs may not know how to run them with parameters, so I will briefly explain.

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

Many people open CMD to**absolute path**Running CloudflareScanner will report an error. This is because the default`-f ip.txt`The parameter is a relative path, and you need to specify the absolute path of ip.txt. However, this is too troublesome, so it is recommended to enter the CloudflareScanner program directory to**relative path**Run as:

**method one**：

1.  Open the directory where the CloudflareScanner program is located
2.  Press on blank space<kbd>Shift + right mouse button</kbd>Show right-click menu
3.  choose**\[Open command window here]**to open the CMD window, which will be located in the current directory by default.
4.  Enter a command with parameters, such as:`CloudflareScanner.exe -tll 50 -tl 200`Ready to run

**Method 2**：

1.  Open the directory where the CloudflareScanner program is located
2.  Select all directly in the folder address bar and enter`cmd`Press Enter to open the CMD window, which will be in the current directory by default.
3.  Enter a command with parameters, such as:`CloudflareScanner.exe -tll 50 -tl 200`Ready to run

> Of course, you can also open a CMD window at will and enter such as`cd /d "D:\Program Files\CloudflareScanner"`to enter the program directory

> **hint**: If using**PowerShell**Just put in the command`CloudflareScanner.exe`Change to`.\CloudflareScanner.exe`That’s it.

</details>

* * *

#### #Windows shortcut to run CloudflareScanner with parameters

If you don’t frequently modify the running parameters (for example, you usually just double-click to run), it is recommended to use the shortcut, which is more convenient.

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

Right click`CloudflareScanner.exe`document -**\[Create Shortcut]**, then right-click the shortcut -**\[Attributes]**, modify its**Target**：

```bash
# If you don't want to output the result file, please add -o " ", where the quotes contain a space (omitting the space will cause this parameter to be omitted).
D:\ABC\CloudflareScanner\CloudflareScanner.exe -n 500 -t 4 -dn 20 -dt 5 -o " "

# If the file path contains quotes, then the startup parameters need to be placed outside the quotes, make sure there is a space between the quotes and -.
"D:\Program Files\CloudflareScanner\CloudflareScanner.exe" -n 500 -t 4 -dn 20 -dt 5 -o " "

# Note! The starting position of the shortcut - cannot be empty, otherwise the ip.txt file will not be found due to the absolute path.
```

</details>

* * *

#### IPv4/IPv6

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

```bash
# You can specify the built-in IPv4 data file to test these IPv4 addresses (-f default value is ip.txt, so this parameter can be omitted)
CloudflareScanner.exe -f ip.txt

# You can specify the built-in IPv6 data file to test these IPv6 addresses
# Additionally, starting from version 2.1.0, CloudflareScanner supports mixed IPv4+IPv6 speed testing and removes the -ipv6 parameter, so one file can contain both IPv4+IPv6 addresses.
CloudflareScanner.exe -f ipv6.txt

# You can also directly specify the IP addresses to be tested through parameters
CloudflareScanner.exe -ip 1.1.1.1,2606:4700::/32
```

> When measuring IPv6 speed, you may notice that the number of speed measurements is different each time. Learn the reason:[#120](https://github.com/Ptechgithub/CloudflareScanner/issues/120)  
> Because there are too many IPv6s (in billions), and most of the IP segments are not enabled at all, I only scanned some of the available IPv6 segments and wrote`ipv6.txt`In the file, those who are interested can scan for additions and deletions by themselves. The ASN data source comes from:[bgp.he.net](https://bgp.he.net/AS13335#_prefixes6)

</details>

* * *

#### #HTTPing

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

There are currently two delayed speed measurement modes, namely**TCP protocol, HTTP protocol**。  
The TCP protocol takes less time, consumes less resources, and has a timeout of 1 second. This protocol is the default mode.  
The HTTP protocol is suitable for quickly testing whether a domain name is accessible when pointing to a certain IP. The timeout is 2 seconds.  
For the same IP, the delay obtained by pinging various protocols is generally:**ICMP &lt; TCP &lt; HTTP**, the further to the right, the more sensitive it is to network fluctuations such as packet loss.

> Note: HTTPing is essentially a**Network scan**behavior, so if you are running on a server, you need**Reduce concurrency**(`-n`), otherwise the service may be suspended by some strict merchants. If you encounter a situation where the number of available IPs in the first HTTPing speed test is normal, and subsequent speed tests are getting less and less or even directly to 0, but then recover after stopping for a period of time, it may be because the operator or Cloudflare CDN thinks you are scanning the network.**Trigger temporary restriction mechanism**, so it will recover after a while, it is recommended**Reduce concurrency**(`-n`) to reduce the occurrence of this situation.

> In addition, this software HTTPing only obtains**response headers**, and does not obtain the body content (that is, the URL file size does not affect the HTTPing test, but if you want to download the speed test, you still need a large file), similar to the curl -i function.

```bash
# Simply add the -httping parameter to switch to HTTP protocol latency testing mode
CloudflareScanner.exe -httping

# The software will determine availability based on the valid HTTP status codes returned when accessing the webpage (of course, timeouts also count). By default, 200, 301, and 302 are considered valid HTTP status codes. You can manually specify valid HTTP status codes, but only one can be specified (you need to determine in advance which status code the test address will return under normal circumstances).
CloudflareScanner.exe -httping -httping-code 200

# Specify the HTTPing test address through the -url parameter (can be any webpage URL, not limited to specific file addresses)
CloudflareScanner.exe -httping -url https://cf.xiu2.xyz/url
# If you want to HTTPing test other websites/CDNs, specify an address used by that website/CDN (because the software's default address is Cloudflare's, it can only be used to test Cloudflare's IPs)

# Note: If the test address is using HTTP protocol, remember to add -tp 80 (this parameter will affect the port used during latency testing/download testing)
# Similarly, if you want to test port 80, you also need to add the -url parameter to specify an address using the http:// protocol (and this address will not be forcibly redirected to HTTPS). If it is a non-80 or 443 port, make sure the download test address supports access through that port.
```

</details>

* * *

#### #Match the specified area (colo airport three-character code)

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

```bash
# This feature supports both Cloudflare CDN and AWS CloudFront CDN, and the three-letter airport codes for these two CDNs are interchangeable.
# Note: If you want to use it to filter AWS CloudFront CDN regions, you need to specify an address using that CDN through the -url parameter (because the default address of the software is Cloudflare's).

# After specifying the region name, the results obtained after latency testing will all be IPs from the specified region (you can also continue to perform download speed tests).
# Node region names are three-letter airport codes, separated by commas when specifying multiple, lowercase letters are supported starting from version 2.2.3.

CloudflareScanner.exe -cfcolo HKG,KHH,NRT,LAX,SEA,SJC,FRA,MAD

# Note that this parameter is only available in HTTPing latency testing mode (because it requires accessing web pages to obtain).
```

> The two CDN airport three-character codes are common, so each region name is visible:<https://www.CloudflareScanneratus.com/>

</details>

* * *

#### File relative/absolute path

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

```bash
# Specify IPv4 data file, do not display results and exit directly, output results to file (-p value is 0)
CloudflareScanner.exe -f 1.txt -p 0 -dd

# Specify IPv4 data file, do not output results to file, display results directly (-p value is 10, -o value is empty but quotes cannot be omitted)
CloudflareScanner.exe -f 2.txt -o "" -p 10 -dd

# Specify IPv4 data file and output results to file (relative path, i.e., in the current directory, if it contains spaces, please enclose it in quotes)
CloudflareScanner.exe -f 3.txt -o result.txt -dd


# Specify IPv4 data file and output results to file (relative path, i.e., in the abc folder in the current directory, if it contains spaces, please enclose it in quotes)
# Linux (in the abc folder within the CloudflareScanner program directory)
./CloudflareScanner -f abc/3.txt -o abc/result.txt -dd

# Windows (note the backslash)
CloudflareScanner.exe -f abc\3.txt -o abc\result.txt -dd


# Specify IPv4 data file and output results to file (absolute path, i.e., in the C:\abc\ directory, if it contains spaces, please enclose it in quotes)
# Linux (in the /abc/ directory)
./CloudflareScanner -f /abc/4.txt -o /abc/result.csv -dd

# Windows (note the backslash)
CloudflareScanner.exe -f C:\abc\4.txt -o C:\abc\result.csv -dd


# If you want to run CloudflareScanner with an absolute path, then the filenames in the -f / -o parameters must also be absolute paths, otherwise an error will occur indicating that the file cannot be found!
# Linux (in the /abc/ directory)
/abc/CloudflareScanner -f /abc/4.txt -o /abc/result.csv -dd

# Windows (note the backslash)
C:\abc\CloudflareScanner.exe -f C:\abc\4.txt -o C:\abc\result.csv -dd
```

</details>

* * *

#### #Test speed of other ports

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

```bash
# If you want to test ports other than the default 443, you need to specify them through the -tp parameter (this parameter will affect the port used during latency testing/download testing).

# If you want to latency test port 80 + download speed (if -dd disables download speed testing, it is not necessary), then you also need to specify an http:// protocol download speed test address (and this address will not be forcibly redirected to HTTPS, because that would become port 443).
CloudflareScanner.exe -tp 80 -url http://cdn.cloudflare.steamstatic.com/steam/apps/5952/movie_max.webm

# If it is a port other than 80 or 443, you need to make sure that the download test address you are using supports access through that non-standard port.
```

</details>

* * *

#### #Custom speed test address

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

```bash
# This parameter is applicable to download speed testing and HTTP protocol latency testing, for the latter, the address can be any webpage URL (not limited to specific file addresses).

# Address requirements: directly downloadable, file size exceeds 200MB, using Cloudflare CDN
CloudflareScanner.exe -url https://cf.xiu2.xyz/url

# Note: If the test address is using the HTTP protocol (this address cannot be forcibly redirected to HTTPS), remember to add -tp 80 (this parameter will affect the port used during latency testing/download testing). If it is a non-80 or 443 port, make sure the download test address supports access through that port.
CloudflareScanner.exe -tp 80 -url http://cdn.cloudflare.steamstatic.com/steam/apps/5952/movie_max.webm
```

</details>

* * *

#### #Custom speed test conditions (specify the target range of latency/packet loss/download speed)

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

> Note: The delay speed test progress bar on the right**Quantity Available**, only refers to the delayed speed measurement process**Number of IPs that have not timed out**, regardless of the delay upper and lower bound conditions.

-   Specify only**[Average latency cap]**condition

```bash
# Maximum average latency: 200 ms, minimum download speed: 0 MB/s
# In other words, find IPs with an average latency below 200 ms, and then perform 10 download speed tests in order of increasing latency.
CloudflareScanner.exe -tl 200
```

> if**No satisfying delay found**conditional IP, nothing will be output.

* * *

-   Specify only**[Average latency cap]**conditions, and**Only delay the speed test, do not download the speed test**

```bash
# Maximum average latency: 200 ms, minimum download speed: 0 MB/s, quantity: unknown
# In other words, only output IPs with an average latency below 200 ms, and no longer perform download speed tests (because download speed tests are no longer performed, the -dn parameter becomes ineffective).
CloudflareScanner.exe -tl 200 -dd
```

-   Specify only**[Maximum packet loss probability]**condition

```bash
# Maximum loss rate: 0.25
# In other words, find IPs with a loss rate lower than or equal to 0.25, range 0.00~1.00. If -tlr 0, it means filtering out any IPs with loss.
CloudflareScanner.exe -tlr 0.25
```

* * *

-   Specify only**[Download speed minimum]**condition

```bash
# Maximum average latency: 9999 ms, minimum download speed: 5 MB/s, quantity: 10 (optional)
# In other words, it needs to find 10 IPs with an average latency below 9999 ms and a download speed higher than 5 MB/s to stop the speed test.
CloudflareScanner.exe -sl 5 -dn 10
```

> if**Didn't find one that met the speed**conditional IP, then it will**Ignore conditions and output all IP speed test results**(This will help you adjust the conditions next time you test your speed).

> When the upper limit of average delay is not specified, if it has been**Not enough**The number of IPs that meet the conditions will**Always measuring speed**Go down.  
> So it is recommended**Specify at the same time[Download speed minimum]+[Average latency cap]**, so that the speed test will be terminated before the specified delay upper limit is reached before sufficient numbers are collected.

* * *

-   Specify at the same time**[Average latency cap]+[Download speed minimum]**condition

```bash
# Maximum average latency and minimum download speed support decimals (e.g., -sl 0.5)
# Maximum average latency: 200 ms, minimum download speed: 5.6 MB/s, quantity: 10 (optional)
# In other words, it needs to find 10 IPs with an average latency below 200 ms and a download speed higher than 5.6 MB/s to stop the speed test.
CloudflareScanner.exe -tl 200 -sl 5.6 -dn 10
```

> if**No satisfying delay found**conditional IP, nothing will be output.  
> if**Didn't find one that met the speed**IP of the condition, then all IP speed test results will be output regardless of the condition (convenient for you to adjust the conditions the next time you test the speed).  
> Therefore, it is recommended to test the speed without specifying conditions first to see what the average delay and download speed are, and avoid specifying conditions.**too low/too high**！

> Because the IP range exposed by Cloudflare is**Back-to-origin IP + Anycast IP**,and**Back to source IP**is unavailable, so the download speed test is 0.00.  
> You can add it at runtime`-sl 0.01`(lower limit of download speed), filter out**Back to source IP**(Results of download speed test below 0.01MB/s).

</details>

* * *

#### Test the speed of one or multiple IPs individually

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

**method one**:
Directly specify the IP segment data to be measured through parameters.

```bash
# First navigate to the directory where CloudflareScanner is located, then run:
# For Windows systems (run in CMD)
CloudflareScanner.exe -ip 1.1.1.1,2.2.2.2/24,2606:4700::/32

# For Linux systems
./CloudflareScanner -ip 1.1.1.1,2.2.2.2/24,2606:4700::/32
```

* * *

**Method 2**:
Or write these IPs into any text file in the following format, for example:`1.txt`

    1.1.1.1
    1.1.1.200
    1.0.0.1/24
    2606:4700::/32

> You can omit it for a single IP`/32`subnet masked (i.e.`1.1.1.1`Equivalent to`1.1.1.1/32`）。  
> subnet mask`/24`Refers to the last segment of this IP, that is`1.0.0.1~1.0.0.255`。

Then add startup parameters when running CloudflareScanner`-f 1.txt`to specify the IP segment data file.

```bash
# First navigate to the directory where CloudflareScanner is located, then run:
# For Windows systems (run in CMD)
CloudflareScanner.exe -f 1.txt

# For Linux systems
./CloudflareScanner -f 1.txt

# For IP ranges like 1.0.0.1/24, only the last segment (1.0.0.1~255) will be randomly selected. If you want to test all IPs in that range, please add the -allip parameter.
```

</details>

* * *

## Manual compilation

<details>
<summary><code><strong>「 Click to expand view content 」</strong></code></summary>

* * *

For convenience, I write the version number into the version variable in the code when compiling, so when you compile manually, you need to add it as follows:`go build`Add after the command`-ldflags`Parameter to specify the version number:

```bash
# Run this command in the CloudflareScanner directory via the command line (e.g., CMD, Bat script) to compile a binary executable program that can run in an environment with the same system, bitness, and architecture as the current device (Go will automatically detect your system bitness and architecture), and the version number will be v2.2.5.

go build -ldflags "-s -w -X main.version=v2.2.5"
```

If you want to compile under Windows 64-bit system**Other systems, architectures, bits**, then you need to specify**GOOS**and**GOARCH**variable.

For example, under Windows system, compile a program suitable for**Linux system amd architecture 64 bit**Binary program for:

```bat
SET GOOS=linux
SET GOARCH=amd64
go build -ldflags "-s -w -X main.version=v2.2.5"
```

For example, under Linux system, compile a program suitable for**Windows system amd architecture 32 bit**Binary program for:

```bash
GOOS=windows
GOARCH=386
go build -ldflags "-s -w -X main.version=v2.2.5"
```

> Can run`go tool dist list`to see which combinations the current Go version supports compiling.

* * *

Of course, in order to facilitate batch compilation, I will specifically specify a variable as the version number, and subsequent compilations can directly call the version number variable.  
At the same time, if you want to compile in batches, you need to put them in different folders (or the file names are different). You need to add`-o`Parameters specified.

```bat
:: For Windows system：
SET version=v2.2.5
SET GOOS=linux
SET GOARCH=amd64
go build -o Releases\CloudflareScanner_linux_amd64\CloudflareScanner -ldflags "-s -w -X main.version=%version%"
```

```bash
# For Linux system：
version=v2.2.5
GOOS=windows
GOARCH=386
go build -o Releases/CloudflareScanner_windows_386/CloudflareScanner.exe -ldflags "-s -w -X main.version=${version}"
```

</details>

* * *

## License

The GPL-3.0 License.
