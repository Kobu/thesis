---
id: research
aliases: []
tags: []
---

#### Existing solutions
As described in Chapter 1, the requirements for a time-tracking application are non-trivial. Luckily there is plenty of existing applications, which promise to deliver just that.
In this chapter we will focus on the introduction and comparison of such application. 

#### Additional requirements
On top of requirements mentioned in the previous chapter, we will judge additional criteria:
##### Speed
It is almost universally accepted, that current web application suffer from being slow. This problem is multi-factorial, and cannot be blamed only one javascript, however the execution of 
javascript code certainly plays a big role. For the end-user, judging if a website is slow is quite a subconcious task. Even non technical users can decide whether a website is slow or not.
However when it comes to optimization we need precise data. A website "being slow" is just not precise enough.

Google having the need to optimze their website, came up in 2020 with Core Web Vitals. Core Web Vitals is a set of user-centered metrics to measure the overall user experience of given website.
There are 3 total metrics
###### Largest Contentful Paint - LPC
LCP measures the required time to render the largest element on a given page. This interval is measured from the time the user requests an URL, to the time the element has finished rendering.
Importance of this metric resides in the fact, that the moment an user requests an url, they start to expect to see something. Having a small button display first is not as important as,
for example, a picture that takes up 75% of the screen. 
User's eyes are most likely going to focus on the picture, not on the small button. Therefore the sooner we can render the picture, the largest element, the 
sooner the user feels like they are experiecing the webpage. Google recognizes LCP of less than 2.5 seconds to be an overally good experience.

###### Interaction to Next Paint - INP
INP is a metric that focuses on the responsiveness of the webpage. It measures the time the webpage takes to respond to user intercations. It is recommended to have INP lesser than 200 miliseconds.
Exceeding this value may not only cause unpleasant user experience, but could straigh up leave to absolute confusion on the user's end. When an user clicks a button, they expect almost immediate feedback
, this can be achieved by using loaders and spinners, to convey the fact that something, in the background is happening.
![spinner.gif](muni/thesis/images/spinner.gif)
Example of an unpleasant experience would be showing a popup dialog one second
after the user has clicked a button, without any loaders or spinners. This causes confusion and bad user experience. Moreover the failure to show that something is happening on the background may
lead to user spamming the button, this can have severe consequences on the integrity of the data the user is modifying.
###### Cumulative Layout Shift - CLS
CLS quantifies visual stability by measuring unexpected layout shifts of visible content on the page. In simpler terms this metric assigns webpage a value between 0 and 1, based on how much
the elements on the webpage shift unexpectedly. Having elements shifted under user's hands not only confuses the user, but may lead to accidental clicks on incorrect elements. The lower the CLS, the better.
General recommendation for CLS is values less than 0.1. As with LPC, spinner or skeletons should be used to prevent high values of CLS. Primary cause of CLS is rendering some elements only after
a fetch call is resloved. This causes the webpage to load, and then shift to account for the element that depends on the fetched data.
![cls.gif](muni/thesis/images/cls.gif)

---
Moreover, there are more web performance metrics we will be interested in:

###### Time To First Byte - TTFB
Measuer the time between the request being sent, and the time when the first byte of the response is being streamed. TTFB lower than 800 miliseconds is considered good

###### First Contentful Paint - FCP
FCP measures the time it takes for any content to be rendered on the screen. A fast FCP (under 1.8 seconds) signals that the page is beginning to load, making users perceive it as more responsive.


In the following comparisons we will use Google's Lighthouse extension for Google Chrome. Lighthouse is a tool to automatically asses a webpage based on several criteria. We will focus on `performance`, which is calculated
based on the above mentioned metric.

##### self-host
In todays cloud-center world, it is often debated who is the actual owner of the data. As an user of some software, not only I want to read my data without filing any GDPR notices, I also want 
to do arbitrary calculation on them. Acquiring personal data is often a lengty process, at least more lengthy than it should, and for those reason a time-tracking application should have the
option to be self-hosted. This way the user truly has control over their data.

##### 3rd party sofware intergration
With software being constantly developed, it is almost impossible to house everything in just one application. And for good reasons. As the unix philosophy goes "an application should do just one thing, and one thing only". 
However, there are times when an user wants data from application to be synced to a totally different application. An example would be usage of Google Calendar and a time tracking application. Data from the time-tracking application
should be synced to the Google Calendar app, so that the end user has absolute overview of what their days look like.
##### overall look and feel, UX
Books should not be judged by the cover, and so should not software application. However nice UI (user interface) and UX (user experience) is crucial for the satifcation of the user. Good looking UI and a simple webpage 
is not an either-or sitation. Quite contrary, good UI should help streamline the navigation on the webpage and help user focus on the elements that matter. For those reasons a time-tracking app should have a simple, good loking UI 
with well thought about UX. 
##### feature-bloat
This requirement goes hand-in-hand with the previous one. Some of the modern web-apps have the curse of feature-bloat. Feature-bloat refers to a application, that just has too many features. This goes directly against the 
saying of doing only one thing, and doing it well, but it also causes cluttered UI with confusing UX. 
##### pricing
Most of the cloud-hosted applications have a paid premium tier TODO


### Solutions
#### track.toggl.com
Toggl Track is one of the most popular time tracking applications. With their phone app having over 1 million dowloads on Google Play Store and chrome extension having over 400 thousand downloads, Toggl Track dominates the market.
The precise amount of their users is unknown, however it is safe to say tha this is the most widely used time tracking application. 


Measuring Toggl with Google Lighthouse, we recieve a performance score of 54/100. This is borderline `poor` score. The main driver of such bad score is LCP. Toggl displays a large calendar on its landing page, this calendar obviously
requires some data to load, which apparently load somewhat slow, hence the bad LCP.

Toggl provides no self-host options, as it is entirely cloud based.

Where Toggl really shines is the integrations. It allows integrations not only with Google and Outlook calendars, but also with additional 100+ application, such as Evernote, Github, GitLab, Notion and much more.

Toggl has a lot of features, some of them are crucial, some are not. This directly causes the UI to be more cluttered than is most likely desired
![toggl.png](muni/thesis/images/toggl.png)

Pricing on toggle is rather generous, the free tier provides regular user with all the features one might desire. 

Summary:
With a company behind this product, it is no wonder the application is this popular. However Toggl's main focus seems to have shifted towards companies. Even the pricing model reflects that as it is tighlty tied to number of users
in a team. That being said, Toggl might be too feature-bloated for users who seek simplicity and straigh-forwardness.


#### traggo
Traggo is an open source, tag-based time tracking tool. It is individual focused, single user app with simplicity in mind. 
![[traggo.png]]
- speed
Thanks to its simplicity, Traggo performance is excellent. With backend written in Go and minimal frontend in Typescript, Traggo manages to be fast and responsive, getting a Lighthouse score of 91.
- self-host
Traggo provides no cloud-hosted option, so the only way to run this application is to self-host it. application is dockerized by default, so the end user can choose whether to run it locally, or on a VPS.
- integrations
Integration is the achilles heel of Traggo, there are basically no built-in intergrations that are supported out of the box.
- UI/UX
The UI/UX delivers what it promises. It is simple, intuitive and visually pleasing.
![traggo.png](muni/thesis/images/traggo.png)
- feature-bloat
Traggo focuses on one thing and one thing only - track time. The whole app is centered around this goal and it does not provide any other features. 
- pricing
Pricing does not applu to Traggo, as it has the need to be self-hosted, one can run it locally.

- summary
Traggo is a good option for users who desire simple, yet powerful way to track their time. The area it lacks in are the integrations, where there are virtually no integrations available. Also users are required to have at least
some level of technical comprehension, because they will need to setup either a VPS provider to host Traggo, or host it locally, which might be a deciding factor for many, as running the app locally prevents users from accessing
their data on multiple devices

TODO: one more comparison


### Conclusion

| App         | Speed     | Self-host | Integrations | UI/UX     | Feature Bloat | Pricing |
| ----------- | --------- | --------- | ------------ | --------- | ------------- | ------- |
| Toggl Track | Mediocre  | None      | Excellent    | Good      | Some          | Fair    |
| Traggo      | Excellent | Full      | None         | Excellent | None          | None    |

Not having found one app to fit all my needs, I decided to develop one on my own. We will follow the requirements mention in the previous two chapters as guidelines.
