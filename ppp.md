<!-- ![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)

<img src="https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif" width="40" height="40" />

<img src="/giphy.gif"/> -->
>## App Introduction
>>Developed by [Max DU](https://github.com/maxdu96)
###### Background: 
Two years ago (in 2022), I couldn’t find a diary record app on mobile that could be added or edited together. Even though Google or Microsoft documents can be shared, they are not real diaries. Secondly, we used the method of sharing a folder in iCloud and typing in notes. However, we found that if there were too many characters on the page, it would lag. So, I got an idea, why can’t I develop one for us?

And here is my app. We released the app in January 2023 as version 1. Since the app connects to Google Firebase, it has a few limits, and if it exceeds them, it will cost money. So for now, I haven’t pushed the app for public use.

There is some features for the app

###### Languages and technology:
+ Swift
+ Node.Js
+ Google Firsbase 
    - Authentication 
    - Firestore Database
    - Functions
    - Messaging

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

##### Demo show:

`welcome page`

<!-- <img src="/giphy.gif"/> -->


show tab 123 and 321
show typing and trash bin
show select date
create a diary
show the list of diary incloud years selector
show diary can edit and delete
show can comments and detele and typing
show can reaction 
diary status have notification
show profile all can editable
show reminder and type and editable
reminder widget and dark mode support, deep link and update and delete
photo mark function
