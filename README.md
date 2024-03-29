<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Requeriments</h3><a id="user-content-get-your-cloudflare-api-key" class="anchor" aria-label="Permalink: Get your Cloudflare API Key" href="#get-your-cloudflare-api-key"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ol dir="auto">
<li>Nginx</li>
<li>Fail2ban</li>
<li>Iptables</li>
<li>A Cloudflare account (<a href="https://www.cloudflare.com/a/sign-up" rel="nofollow">https://www.cloudflare.com/a/sign-up</a>)</li>
</ol>

<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Get your Cloudflare API Key</h3><a id="user-content-get-your-cloudflare-api-key" class="anchor" aria-label="Permalink: Get your Cloudflare API Key" href="#get-your-cloudflare-api-key"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ol dir="auto">
<li>
<p dir="auto">Signup to Cloudflare: <a href="https://www.cloudflare.com/a/sign-up" rel="nofollow">https://www.cloudflare.com/a/sign-up</a></p>
</li>
<li>
<p dir="auto">Go to <a href="https://www.cloudflare.com/a/account/my-account" rel="nofollow">https://www.cloudflare.com/a/account/my-account</a> and select <code>View API Key</code>.</p>
</li>
<li>
<p dir="auto">Setup your site(s) to use Cloudflare</p>
</li>
</ol>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Configure Nginx</h3><a id="user-content-configure-fail2ban" class="anchor" aria-label="Permalink: Configure Fail2ban" href="#configure-fail2ban"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ol dir="auto">
<li>
<p dir="auto">Add the following to your <code>nginx.conf</code> file:</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto" data-snippet-clipboard-copy-content="
    set_real_ip_from 127.0.0.1;
    set_real_ip_from 173.245.48.0/20;
    set_real_ip_from 103.21.244.0/22;
    set_real_ip_from 103.22.200.0/22;
    set_real_ip_from 103.31.4.0/22;
    set_real_ip_from 141.101.64.0/18;
    set_real_ip_from 108.162.192.0/18;
    set_real_ip_from 190.93.240.0/20;
    set_real_ip_from 188.114.96.0/20;
    set_real_ip_from 197.234.240.0/22;
    set_real_ip_from 198.41.128.0/17;
    set_real_ip_from 162.158.0.0/15;
    set_real_ip_from 104.16.0.0/13;
    set_real_ip_from 104.24.0.0/14;
    set_real_ip_from 172.64.0.0/13;
    set_real_ip_from 131.0.72.0/22;
    set_real_ip_from 2400:cb00::/32;
    set_real_ip_from 2606:4700::/32;
    set_real_ip_from 2803:f800::/32;
    set_real_ip_from 2405:b500::/32;
    set_real_ip_from 2405:8100::/32;
    set_real_ip_from 2a06:98c0::/29;
    set_real_ip_from 2c0f:f248::/32;
    real_ip_header X-Forwarded-For;
    #real_ip_header CF-Connecting-IP;
    real_ip_recursive on; ">
<pre class="notranslate"><code>## Real IP Forwarding ##
    set_real_ip_from 127.0.0.1;

    # CloudFlare IPs
    # List from: https://www.cloudflare.com/ips-v4
    set_real_ip_from 173.245.48.0/20;
    set_real_ip_from 103.21.244.0/22;
    set_real_ip_from 103.22.200.0/22;
    set_real_ip_from 103.31.4.0/22;
    set_real_ip_from 141.101.64.0/18;
    set_real_ip_from 108.162.192.0/18;
    set_real_ip_from 190.93.240.0/20;
    set_real_ip_from 188.114.96.0/20;
    set_real_ip_from 197.234.240.0/22;
    set_real_ip_from 198.41.128.0/17;
    set_real_ip_from 162.158.0.0/15;
    set_real_ip_from 104.16.0.0/13;
    set_real_ip_from 104.24.0.0/14;
    set_real_ip_from 172.64.0.0/13;
    set_real_ip_from 131.0.72.0/22;

    # List from: https://www.cloudflare.com/ips-v6
    set_real_ip_from 2400:cb00::/32;
    set_real_ip_from 2606:4700::/32;
    set_real_ip_from 2803:f800::/32;
    set_real_ip_from 2405:b500::/32;
    set_real_ip_from 2405:8100::/32;
    set_real_ip_from 2a06:98c0::/29;
    set_real_ip_from 2c0f:f248::/32;

    # Replace with correct visitor IP
    real_ip_header X-Forwarded-For;
    real_ip_recursive on;
</code></pre></div>
</li>
</ol>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Configure Fail2ban</h3><a id="user-content-configure-fail2ban" class="anchor" aria-label="Permalink: Configure Fail2ban" href="#configure-fail2ban"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ol dir="auto">
<li>
<p dir="auto">Install <code>Fail2ban</code> on the server running Nginx.</p>
</li>
<li>
<p dir="auto">Add the <code>nginx-dos.conf</code> file to your <code>filter.d</code> dir.</p>
</li>
<li>
<p dir="auto">Add the <code>cloudflare-restv4.conf</code> file to your <code>action.d</code> dir.</p>
</li>
<li>
<p dir="auto">Add the following to your <code>jail.conf</code> file:</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto" data-snippet-clipboard-copy-content="[nginx-dos]
enabled = true
filter  = nginx-dos
action = iptables-multiport[name=HTTP, port="http,https", protocol=tcp]
         cloudflare-restv4[cfuser="YOUR CLOUDFLARE EMAIL", cfkey="YOUR CLOUDFLARE API KEY", cfzone="YOUR CLOUDFLARE ZONE"]
logpath = /var/log/nginx/access.log
findtime = 10
bantime  = 1800
maxretry = 20">
<pre class="notranslate"><code>[nginx-dos]
enabled = true
filter  = nginx-dos
action = iptables-multiport[name=HTTP, port="http,https", protocol=tcp]
         cloudflare-restv4[cfuser="YOUR CLOUDFLARE EMAIL", cfkey="YOUR CLOUDFLARE API KEY", cfzone="YOUR CLOUDFLARE ZONE"]
logpath = /var/log/nginx/access.log
findtime = 10
bantime  = 1800
maxretry = 150
</code></pre></div>
  </li>
<li>
<p dir="auto">Configure <code>cloudflare-restv4.conf</code> replace <code>YOUR CLOUDFLARE EMAIL</code>, <code>YOUR CLOUDFLARE API KEY</code>, <code>YOUR CLOUDFLARE ZONE</code> with your email, api key and zone used in cloudflare.</p>
</li>
<li>
<p dir="auto">Restart <code>Fail2ban</code>.</p>
</li>
</ol>
<p dir="auto">This will make <code>Fail2ban</code> monitor the file <code>/var/log/nginx/access.log</code> and each client with more than 150 attempts will be banned on <code>cloudflare</code> and <code>iptables</code> for 1800 seconds (30 minutes).</p>
<p dir="auto">It might be a good idea to whitelist the IP range of Cloudflare in <code>Fail2ban</code> using the <code>ignoreip</code> section. A current list of the IP ranges of Cloudflare can be found here: <a href="https://www.cloudflare.com/ips/" rel="nofollow">https://www.cloudflare.com/ips/</a></p>
<p dir="auto">NOTE: At the moment <code>Fail2ban</code> doesn't work with IPv6 so it might be a good idea to disable IPv6 support in the Cloudflare admin interface for each site you want to protect using Fail2ban.</p>
