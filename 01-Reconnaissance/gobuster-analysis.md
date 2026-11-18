
# Gobuster Directory Enumeration Analysis

## 1. Target Information
- Target Application: OWASP Juice Shop
- Target URL: http://127.0.0.1:3000
- Target IP: 127.0.0.1
- Testing Environment: Local Docker Lab

## 2. Tool Information
- Tool: Gobuster
- Version: 3.8.2
- Mode: Directory Enumeration
- Wordlist: /usr/share/wordlists/dirb/common.txt
- Threads: 20
- Excluded Response Length: 9984

## 3. Scan Command
gobuster dir -u http://127.0.0.1:3000 -w /usr/share/wordlists/dirb/common.txt -t 20 --exclude-length 9984 -o gobuster-scan.txt

## 4. Discovered Paths

| Path | Status Code | Response Size |
|---|---:|---:|
| /api | 500 | 2408 |
| /apis | 500 | 2410 |
| /assets | 301 | 156 |
| /ftp | 200 | 11318 |
| /media | 301 | 155 |
| /profile | 500 | 1043 |
| /promotion | 200 | 5863 |
| /redirect | 500 | 2531 |
| /restaurants | 500 | 2424 |
| /rest | 500 | 2410 |
| /restore | 500 | 2416 |
| /restricted | 500 | 2422 |
| /restored | 500 | 2418 |
| /robots.txt | 200 | 28 |

## 5. Key Observations
1. Multiple application paths were discovered.
2. The /ftp and /promotion paths returned HTTP 200.
3. The /robots.txt file is publicly accessible.
4. The /assets and /media paths returned HTTP 301 redirects.
5. Several paths returned HTTP 500 errors.
6. The application returned a wildcard response for nonexistent paths, requiring response-length filtering.

## 6. Scan Limitations
Several requests encountered timeouts, connection resets and unexpected EOF errors during scanning. These may indicate connection instability or server-side request handling limitations.

## 7. Initial Security Assessment
The discovered paths require further manual verification. HTTP status codes alone do not confirm security vulnerabilities.

Priority areas for further investigation:
- /ftp
- /robots.txt
- /api
- /assets
- /media

## 8. Conclusion
Gobuster successfully completed directory enumeration against the local OWASP Juice Shop application and identified 14 paths for further investigation.

## 9. Evidence
- Raw scan output: gobuster-scan.txt
