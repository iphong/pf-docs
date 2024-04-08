---
description: A way to set up sustainable tunnel URL while starting the development server
---

# Set up tunnel Cloudflared with Partial DNS (CNAME Setup)

This article will guide us on how to connect your tunnel CloudFlared to a custom domain & reduce the time of starting the developing environment by manually running `ngrok http 3000` or re-creating Cloudflare tunnel if our system re-boots or catches a network error. Beyond that, the tunnel will be sustainable as your domain, with **NO random URL anymore**.

A brief description of what this instruction does, as we already know that in order to run a **Shopify App Development**, we need a domain that valid with a TLS certificate so the domain must be display HTTPS. For serving our app over HTTPS using a valid TLS certificate, we can create our own certificate, or on the other hand, and make our life a little bit easier, we can use some external services like `ngrok`, or `Cloudflared` - which are very similar to us.

### Prelude

Let's remind the process of starting a tunnel&#x20;

Here is the [basic setup](https://dashboard.ngrok.com/get-started/setup/macos) with `ngrok`

*   Install `ngrok` via Homebrew with the following command:

    `brew install ngrok/ngrok/ngrok`
*   Run the following command to add your auth token to the default `ngrok.yml` configuration file

    `ngrok config add-authtoken 2Cn7FPruN7OXJhj5RYJRvSPHF6b_lisandro`

> [_Homebrew - The Missing Package Manager for macOS (or Linux)_](https://brew.sh/) _I would highly recommend that we should install this tool to install external packages easier_

But it has a CONS, if we turn off our machine or environment, we must manually restart the `ngrok` URL so the URL will be changed and it's not fancy in case we're working with some services needing a persistent URL.

So what we can do now? How to make the URL never change? Or you're finding a way to help you reduce your time in starting the development environment. This article is for you, you're standing in correct way.



### Lease a domain

Ok, I clearly understand & agree that this way will make us pay/purchase some efforts, BUT we can easily find a cheap domain only from `1.98$/year`

![Example of leasing a domain](https://img001.prntscr.com/file/img001/0bVrrWcpTQap\_RNJ9pi2eg.png)

We can slightly find some services like Google Domain, Namecheap,...

In this case, I use Google Domain as a service served for me.

After finishing the process of buying a domain, we need to configure the DNS (Domain Name System), we will point the Cloudflare tunnel to your domain. Let's remain this tab, we will set up this configuration later.



### Config tunnel in Cloudflare <a href="#markdown-header-config-tunnel-in-cloudflared" id="markdown-header-config-tunnel-in-cloudflared"></a>

#### Login Cloudflare <a href="#markdown-header-login-cloudflared" id="markdown-header-login-cloudflared"></a>

> _**If this is the first time you get acquainted with Cloudflared, don't worry, I will help you step-by-step, unless you can skip this section.**_

First, you register your Cloudflare account in [dash.cloudflare.com](https://dash.cloudflare.com/login)

After logging into Cloudflare successfully, you will see the main dashboard

#### Add site to Cloudflare <a href="#markdown-header-add-site-to-cloudflared" id="markdown-header-add-site-to-cloudflared"></a>

In the [dashboard](https://dash.cloudflare.com/), we can slightly see the primary button **Get Started** in the section `Add a website...`

1. Click on the button **Get started**
2. Add your domain registered -> Click **Continue**

![alt text](https://img001.prntscr.com/file/img001/8ZSKu-4OTSSwKKI4vpKHuA.png)

3. Select Plan

Choose the **FREE** option for sure -> Click **Continue** -> Wait about 1-2 minutes for this process

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>Select plan image</p></figcaption></figure>

4. Review DNS records

We can skip this process at this time, I will come back to this essential process later.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>DNS records image</p></figcaption></figure>

5. Change your nameservers

You will see that Cloudflared provides us with two Cloudflared nameservers, our mission is to assign these nameservers to domain services.

Click copy nameservers step-by-step. Remember the Google Domain tab that previously I mentioned before, let's come back to this tab and paste these nameservers into `DNS` tab.

**From Cloudflare:**

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Cloudflare nameservers image</p></figcaption></figure>

**From Google Domain:**

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Assign DNS</p></figcaption></figure>

After finishing these above steps, come back to **Cloudflare** -> Click the button `Check nameservers now` to verify that your domain is pointing correctly & robust to CloudFlare. If the status is OK, let `continue` again, then you will see some configurations to make your site more secure. I will remain these options by default.

> _It can let us **wait 24 hours** for registrars take up to process nameserver changes._

![The screen if your Cloudflare is pointing to your site](https://img001.prntscr.com/file/img001/5S-8fOfNQI2mHSC8y2FEjw.png)

#### Set up the Zero Trust <a href="#markdown-header-set-up-the-zero-trust" id="markdown-header-set-up-the-zero-trust"></a>

Let's take a brief about Zero Trust. What is this? Zero Trust **is a security model based on the principle of maintaining strict access controls and not trusting anyone by default, even those already inside the network perimeter**.

So we can configure the network tunnel in this feature. Click **Zero Trust** -> **Networks** -> **Tunnels** -> **Add a tunnel**

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Tunnel in Zero Trust</p></figcaption></figure>

1. **Select tunnel type**\
   Select the option recommended&#x20;

<figure><img src="https://img001.prntscr.com/file/img001/YTBZ1GoQQWSpWuuy3A_qVQ.png" alt=""><figcaption><p>Select tunnel type</p></figcaption></figure>

2. **Name tunnel**\
   Inputting the name that you want

![Naming for tunnel](https://img001.prntscr.com/file/img001/mGJb0TN3Rh2Ms-uoAdlnGw.png)

3. **Install and run the connectors**

* Choose your environment, in this case, I choose the MAC because I'm a MAC user. Please select the environment that is appropriate.
* Connect tunnel to Cloudflare
  * Cloudflared provides us with two options to connect, the first case is installing the Cloudflared CLI and starting the services on your local environment, and the second is starting the services directly without installing the Cloudflared CLI.
  * Select the option that is suitable for you -> **Copy option** -> **Paste** to your terminal.

**From Cloudflare**

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>Install &#x26; start the cloudflared service</p></figcaption></figure>

**From terminal**

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>Status of installing &#x26; starting the cloudflared service</p></figcaption></figure>

{% hint style="info" %}
As we can see cloudflared client is running as a system launch daemon, which means cloudflared client will run at boot, whenever your system starts, it will automatically run as a service, we don't need to manually start a tunnel again. Cool, right?
{% endhint %}

*   Add public hostname

    * After connecting the tunnel to Cloudflare, you will need a public host site in order to establish a secure connection between Cloudflare's edge and your infrastructure.
    * Click the **Add a Public Host Name** button

    &#x20;\


    <figure><img src="https://img001.prntscr.com/file/img001/63b5C5DsR_-Ujl_xhU_Jfw.png" alt=""><figcaption><p>Public Hostname Screen</p></figcaption></figure>
* Now we need a **subdomain** name based on your site, type is `HTTP`, and example for the URL will need a `PORT` to specify which application's port is running. In this case, I will change it to `3000` by default of the project configuration -> **Save** **hostname**.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>Configure Public Hostname Page</p></figcaption></figure>

Now we can start the server or our application, `pfserver` in this case with a very elegant command

`npm run dev-shopify -- --tunnel-url https://pf.longpc.dev:3000`



### Healthy tunnel check-up

We can check the tunnel if it's robust, by going to the specific tunnel -> **Status**

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Tunnel's health</p></figcaption></figure>

### Advanced <a href="#markdown-header-advanced" id="markdown-header-advanced"></a>

#### Development mode

This mode will temporarily bypass our cache allowing you to see changes to your origin server in real time.

<figure><img src="https://img001.prntscr.com/file/img001/hGWvmKs7RraafdTdYsm8PQ.png" alt=""><figcaption><p>Development mode</p></figcaption></figure>

> _If you want to know why we need this mode, please take a glance at this_ [_issue_](https://bravebits.jira.com/issues/PFSHOPIFY-5582)_._

### Related topics

#### 1. [Run tunnel whenever your system boots](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/configure-tunnels/local-management/as-a-service/macos/) <a href="#markdown-header-run-tunnel-whenever-your-system-boots" id="markdown-header-run-tunnel-whenever-your-system-boots"></a>
