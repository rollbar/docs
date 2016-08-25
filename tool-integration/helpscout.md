## Using Rollbar inside Help Scout

If you use [Help Scout](https://www.helpscout.net/) for support, you can
integrate it with Rollbar to see recent errors that affected your users
who write in to support. We use this ourself and love it.

The Rollbar app will appear on the right sidebar in the Conversation
view. It looks like this:

![](http://photos.osmek.com/helpscout_1.133226.o.png)

### Setup Instructions

Note that this requires a paid Help Scout account.

1.  In HelpScout, click Apps in the top bar

    ![](http://photos.osmek.com/helpscout_3.133228.o.png)

2.  Click "Build a Custom App"

    ![](http://photos.osmek.com/helpscout_4.133229.o.png)

3.  Click "Create App".

    ![](http://photos.osmek.com/helpscout_5.133230.o.png)

4.  Fill out the form as follows. Make sure to replace
    PROJECT\_READ\_ACCESS\_TOKEN with a 'read' scope access token for
    the relevant project.

    -   App Name: Rollbar
    -   Content Type: Dynamic Content
    -   Callback
        Url: <https://rollbar.com/callback/helpscout/PROJECT_READ_ACCESS_TOKEN>
    -   Secret Key: PROJECT\_READ\_ACCESS\_TOKEN
    -   Debug Mode: Off
    -   Mailboxes: check all

     ![](http://photos.osmek.com/helpscout_2.133227.o.png) 

5.  Press "Save".

 

Now when you navigate to a conversation in Help Scout, you'll see the
Rollbar app showing the most recent 10 occurrences that affected the
user who started the conversation.
