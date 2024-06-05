# [Slack Alfred Workflow](https://renatomoor.github.io/slack-alfred-workflow/)

Introducing the Slack Search Workflow for Alfred, 
a powerful and efficient way to quickly search for 
users and channels in your Slack workspace. By leveraging 
the power of Alfred and the Slack API, this workflow simplifies 
your Slack experience and boosts productivity. With just a few 
keystrokes, you can easily navigate through your workspace and find 
the conversations you need.

Requirements
- Alfred Powerpack
- Homebrew
- Slack workspace
- Creating and adding a Slack app to your workspace

Installation: [Slack Alfred Workflow](https://renatomoor.github.io/slack-alfred-workflow/)

Note: This workflow is not affiliated with or endorsed by Slack Technologies, Inc.

<a href="https://www.buymeacoffee.com/renatomoor" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" height="41" width="174"></a>



---
# How to import slack private channel

Since the original project has been closed, I'm just Forking it over to share how to import slack private channel.

1, Open The Slack on browser
https://app.slack.com/client/


2, Open the browser console

3, Run the following code to get the channel list

```code
// Function to create formatted channel strings
function genChannelCode(name, teamId, channelId) {
    return `items.push(genCustomChannel("${name}", "${teamId}", "${channelId}"))`;
}

// Main function to extract data from the DOM
function extractChannelData() {
    const teamId = new URL(window.location.href).pathname.split('/')[2]
    const items = [];  // Array to store final results
    const channels = document.querySelectorAll('.p-channel_sidebar__channel'); // Select all channel DOM elements

    channels.forEach(channel => {
        const lockIcon = channel.querySelector('[data-sidebar-channel-icon="lock"]'); // Check for the lock icon
        if (lockIcon) {
            const channelName = channel.querySelector('.p-channel_sidebar__name').textContent.trim(); // Get channel name
            const channelId = channel.getAttribute('data-qa-channel-sidebar-channel-id'); // Get channel ID
            const channelOutput = genChannelCode(channelName, teamId, channelId); // Format output
            const slackLink = `https://app.slack.com/client/${teamId}/${channelId}`; // Assume team ID is fixed
            items.push(`${channelOutput};//${slackLink}`); // Add formatted string to array
        }
    });
    console.log(items.join('\n'));
}

// Execute function
extractChannelData();
```

then you will get the output like this

```code

items.push(genCustomChannel("channel1", "XXX", "YYY"));//https://app.slack.com/client/XXX/YYY
items.push(genCustomChannel("channel2", "XXX", "ZZZ"));//https://app.slack.com/client/XXX/YYY
```


4, Copy the output and paste it to the `store\channels.js` file

5, Run `update slack users and channels` in Alfred

6, Done

---