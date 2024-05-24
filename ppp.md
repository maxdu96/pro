<!-- ![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)

<img src="https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif" width="40" height="40" />

<img src="/giphy.gif"/> -->
>## App Introduction
>>Developed by [Max DU](https://github.com/maxdu96)
###### Background: 
Two years ago(in 2022), I can’t find some diary record app in mobile. Because I need the app can be add or edit with together. Even google or Microsoft documents can do the share, but not a real diary. 其次就是 icloud share folder and type in 備忘錄, in passing days, we use this method to do. But we though that if too many character on the page, it will so lag. So I get an Idea, why I can’t develop one for our?

And here is my app. We have been release the app on 01/2023 version 1. Since the app will connect google firebase, it has a few limit, if over then will be 收錢. So for now, I don’t push the app for public.

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
