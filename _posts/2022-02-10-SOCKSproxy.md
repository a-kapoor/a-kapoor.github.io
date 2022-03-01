# **Browsing the web via a SOCKS proxy**

**Step 1:**

On a terminal on your local machine outside CERN network, do this
```ssh -D 1080 username@hostname```

For lxplus, just do

```ssh -D 1080 username@lxplus.cern.ch```

If 1080 is being used already, just use some random large number. Like 5040

**Step 2:**

Then (for firefox), go to

```Edit -> Preferences -> "Advanced" category -> "Network Settings" button```

On different versions of firefox, the steps to reach network settings might be dfferent.

Most important:
Then choose "manual proxy configuration" and enter host as **localhost** and port **1080** as SOCKS host information. You only need to do this once.

I have automated the whole process on my machine. So as soon as I open my machine, Step 1 happens automatically and I am good to go. You may do the same.

That's it. Happy browsing.

