# Gifting a White Elephant

Web, 200 points

## Description:

Ok, everyone, I've got a really cool challenge for this one but I need everyone to not rat me out. For this challenge, I've decided to put you in the shoes of an investigator looking to take down a website that hosts illegal content. In this case, a forum that posts carding data. Your task is to probe the site for evidence and identify every subject.

I wanted this to be as real as possible, so I've got hundreds of users, dozens of moderators, and the kingpin site administrator. I've got dozens of pages, hundreds of clues, and it's a full multimedia site. Which is why I need you to be cool about this and not go blabbing about this challenge, because in order to make the scenario as real as possible I'm using real data from real cases. I realize that this is, technical speaking, mega-illegal, but I wanted a cool challenge. I guess I could have created simulated evidence, but... eh... Sounds like a lot of work and to be honest I'm just over it. It's whatever, just keep it to yourself and it'll be fine.

## Solution:

We visit the website and get the following page:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Site Seized</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        text-align: center;
        background-color: white;
        color: black;
        padding: 20px;
      }
      .warning-header {
        color: red;
        font-size: 1.5em;
        font-weight: bold;
        text-transform: uppercase;
        margin-top: 30px;
        border-bottom: 2px solid black;
        padding-bottom: 10px;
      }
      .seized-notice {
        font-size: 2em;
        font-weight: bold;
        color: darkred;
        margin: 20px 0;
      }
      .description {
        font-size: 1.2em;
        color: #333;
        margin: 15px 0;
      }
      .agency-logos img {
        width: 150px;
        margin: 10px;
      }
      .footer {
        font-size: 0.9em;
        color: #666;
        margin-top: 40px;
      }
    </style>
  </head>
  <body>
    <div class="warning-header">This Website Has Been Seized</div>

    <div class="seized-notice">
      Under the authority of the Federal Bureau of Investigation (FBI)
    </div>

    <p class="description">
      As part of a law enforcement operation, this domain has been seized by the
      FBI due to involvement in illegal activities. Unauthorized access or
      attempts to restore this website without federal authorization is a
      violation of federal law.
    </p>

    <div class="agency-logos">
      <img src="/static/FBI_Logo.png" alt="FBI Logo" />
      <img src="/static/DOJ_Logo.png" alt="DOJ Logo" />
    </div>

    <p class="footer">
      For further information, please visit the official website of the FBI or
      Department of Justice.
    </p>
    <!-- Agent access only -->
    <a href="/agent-access"></a>
  </body>
</html>
```

We can see that there is a hidden link navigating to `/agent-access`

We navigating to that link we get the following page:

```html
<!DOCTYPE html>
<h3>Access Denied</h3>
<p>
  Unauthorized access attempt has been logged. Federal authorities have been
  notified. If you are authorized to view this page, please ensure you are using
  the department mandated browser
  <br />
  Err: 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko)
  Chrome/131.0.0.0 Safari/537.36'
  <script>
    console.warn(
      "Not FBI-SiteAccess-Authorized-Agent. Unauthorized access detected. User agent mismatch. 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36'"
    );
  </script>
</p>
```

To solve this challenge we need to use a tool like BurpSuite to modify our User-Agent to be ```FBI-SiteAccess-Authorized-Agent```

Once we complete that, we can access the flag. 

The flag: `poctf{uwsp_4_fr13nd_70_4ll}`
