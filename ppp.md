<!-- ![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)

<img src="https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif" width="40" height="40" />

<img src="/giphy.gif"/> -->
># App Introduction
>>Developed by [Max DU](https://github.com/maxdu96)
#### Background: 
Two years ago (in 2022), I couldn’t find a diary record app on mobile that could be added or edited together. Even though Google or Microsoft documents can be shared, they are not real diaries. Secondly, we used the method of sharing a folder in iCloud and typing in notes. However, we found that if there were too many characters on the page, it would lag. So, I got an idea, why can’t I develop one for us?

<img src = "/Image/git_first.jpg" />
<img src = "/Image/git_version1.0.jpg" />
And here is my app(Project Created on Sep 2023). We released the app in Dec 2023 as version 1.0. 

#### Languages and technology:
+ Swift
+ Node.Js 18
+ Google Firsbase 
    - Authentication 
    - Firestore Database
    - Functions
    - Messaging
+ GitHub Source Control

#### App Status
It is expected to be launched on the App Store in October 2024 and already has a new UI.

___

*The app can make the couple record there are daily life together. All can access create or edit one diary. Or maybe say, people often forget what they do on a day. So when they wanna remember that day, they can open the app to check, can let them happy or xxx one more time. And the couple for two both have responsibility to do this things*

___

#### There are some features of the app:

##### Demo show:

| Option  | Description |
| ------ | :-----------: |
| `Welcome page & App basic` | <img src="/Image/GIF/welcome.gif" width="30%" height="30%" /> <img src="/Image/GIF/main_3tab.gif" width="30%" height="30%" />|
| `Diary create flow` | <img src="/Image/GIF/diary_typing.gif" width="30%" height="30%" />  <img src="/Image/GIF/day_range_selector.gif" width="30%" height="30%" /> <img src="/Image/GIF/diary_create.gif" width="30%" height="30%" />|
| `Diary list show` | <img src="/Image/GIF/diary_read.gif" width="30%" height="30%" /> <img src="/Image/GIF/year_selector.gif" width="30%" height="30%" /> <img src="/Image/GIF/diary_canEdit.gif" width="30%" height="30%" />|
| `Comment functions` | <img src="/Image/GIF/coment_typing.gif" width="30%" height="30%" /> <img src="/Image/GIF/coment_reaction.gif" width="30%" height="30%" />  <img src="/Image/GIF/comment_count.gif" width="30%" height="30%" /> |
| `Diary status have remote notification` | <img src="/Image/GIF/notif_create.gif" width="30%" height="30%" /> <img src="/Image/GIF/notif_edit.gif" width="30%" height="30%"/> <img src="/Image/GIF/notif_reaction.gif" width="30%" height="30%" />|
| `Profile all can be editable` | <img src="/Image/GIF/profile_canEdit.gif" width="30%" height="30%" /> |
| `Reminder widget and deepLink` <br> If you ask me why I don't use the native "Reminder" feature of Apple, it's because the native "Reminder" updates a "completed task" on the left side, and it's very easy to accidentally click on it in the widget. ^ ^  | <img src="/Image/GIF/reminder_typing.gif" width="30%" height="30%" /> <img src="/Image/GIF/reminder_widget.gif" width="30%" height="30%" /> <img src="/Image/GIF/reminder_widgetColor.gif" width="30%" height="30%" /> <img src="/Image/GIF/reminder_widgetUpdate.gif" width="30%" height="30%" /> <img src="/Image/GIF/reminder_widgetDeeplink.gif" width="30%" height="30%" />|
| `photo mark function` | <img src="/Image/GIF/photo_mark.gif" width="30%" height="30%" /> |
<!-- | `Photo mark Widget` | Coming soon | -->

___
##### REST API and FCM example (Node.Js):

``` js
app.post('/', async (req, res) => {
    const date = req.body.date;
    const content = req.body.content;
    const authorID = req.body.authorID;

    if (date == null || content == null || authorID == null) {
        return res.status(400).send({"message":"Error, have nil value！"});
    }

    var diary = {"date":date, "content":content, "authorID": authorID};
    await admin.firestore().collection('Diaries_Test').add(diary);
    res.status(201).send({"message":"Diary insert successful！"});
});
```

``` js
  const message = {
      notification: {
        title: userName,
        body: `寫咗新日記：${diaryContent}`,
      },
      data: {
        docId: docId,
        route_diaryContent: diaryContent,
        route_date: route_date,
        route_authorID: authorID
      },
      android: {
        notification: {
          imageUrl: userIcon
        }
      },
      apns: {
        payload: {
          aps: {
            'mutable-content': 1
          }
        },
        fcm_options: {
          image: userIcon
        }
      },
      webpush: {
        headers: {
          image: userIcon
        }
      },
      topic: 'all'
    };
    await admin.messaging().send(message);
```

