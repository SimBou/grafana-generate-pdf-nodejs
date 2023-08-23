# Grafana PDF Report using Puppeteer

Generate pdf report for grafana dashboards using nodejs and puppeteer.

I took the base code from
<https://gist.github.com/svet-b/1ad0656cd3ce0e1a633e16eb20f66425>

It was generating blank panels after certain point when dashboard is tall. This repo code addresses this issue.

## Automated PDF export of Grafana dashboard using Puppeteer

### Prerequisites

General:
- Grafana server with dashboards that are to be exported, and datasources in "Server" (proxy) mode.
- User account on Grafana server that has Viewer access to the required dashboards
- This has been tested on Ubuntu 16.04 and a Mac

Packages:
- NodeJS, and the `puppeteer` package (`npm install puppeteer`), which is used to run headless Chrome
- In Linux, Puppeteer has the following library/tool dependencies (primarily related to `libx11` - see [this post](https://techoverflow.net/2018/06/05/how-to-fix-puppetteer-error-while-loading-shared-libraries-libx11-xcb-so-1-cannot-open-shared-object-file-no-such-file-or-directory/)). I found that I didn't need extra packages on a Mac.
```
sudo apt-get install gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget
```

Scripts:
- The [grafana_pdf.js](https://gist.githubusercontent.com/svet-b/1ad0656cd3ce0e1a633e16eb20f66425/raw/grafana_pdf.js) file attached here, which carries out the PDF conversion using Puppeteer

### You can directly run this command by passing all the params

``` sh
node grafana_pdf.js "http://localhost:3000/d/7ps_KoFMk?orgId=1&from=1602513421982&to=1602513601734" token output/grafana_dash.pdf

node grafana_pdf.js "http://localhost:3000/d/VyLxLpNnk/first?orgId=1" token output/grafana_dash.pdf
```

### or you can set some env variables shown below

Environment: Set the Grafana server URL, username, and password, and the output filename as environment variables.

``` sh
export GF_DASH_URL="http://localhost:3000/d/x3g4Wx5ik/new-dashboard?kiosk"
export GF_TOKEN=frqcfqsdf45fqsdfq1vdfq2dqxfq3ht
export OUTPUT_PDF=output/output.pdf

# Now export to PDF by calling the NodeJS script with the corresponding arguments:

node grafana_pdf.js $GF_DASH_URL $GF_TOKEN $OUTPUT_PDF

```
